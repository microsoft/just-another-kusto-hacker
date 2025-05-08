[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHVUwY7TMBC95ysGJKQEDLUdJ3FA4cKFEwdW4oLQyk2mrSGxK8dlu4iPZ9Jmm+yBW2y/ee/Nm2mTzaY1fXvqTUSIB4TxaKI1PQQ8BhzRRTp6B36XbDb4m84jPbU+dNiBaYMfR4h2QAa997+s24OJsLMO3+6DsY6KOnp1I3GY3sbHdwDfLD5cpVoTI4b2YEJ8l/QYYRZooDOka7Y9ptG2vz75k4vve+/2GXxPZFHngheikkozqbWsKyFlXVa5FCVnsqg0l1XNVSnpUCtRlLlQkrPkcqqKuqhLxSRVVaUmHqWk4PV8U9S80mWtC07lRa5knZNcKeVcXnKRa6nmpyIvNXHltapkJUvJJztKsbLSkqtCS5nrWpKrROW1JkuKkyYjVbIriryWKldC84JRC6UWBa8rKZMf8BdGDDQH+wfpG88RXQe3KJvgH+7dadhiSLMPl+imnL4at8cmegq2NyG9pklMp2EwYWIaXDNYt2SaseHcDOa8ukluaq4ZY6ARpdEf8JwO54zNXy7LyNQx+J/YRnCzg5u7aYBhsgId7IIfgEP0UOYwRjyCWPpBu0f3mzh8aMSVxJzt+MUMuHDYFQcZ6vHq/9JrNlMupqf6hjreEpS2cYEyy8SquZtZ0ol+Wq107vYlP79kEw01+SFZ/PyFn946oB3vqMY6h+FpX4nlxkcS048jwPaRrJux/U+7yYqvubKtAiTGFXqxfUfSW+tMeLwfD3YX73vcxVSwbtXaZ2hmiHHdMll2N2EeDhgQPr9o+OLraKeG4BWIfBVkaOm2NSNCaj829Mb4swTx1JPnBtKjfS14Bm8A9FtIO+LRK9hg9s7GU4fQpMQ5Qd9MqM0zFGU/DcnhOF4GMk/vYopPuKdlu6iyGylbFRIqEBeZWv+xwIONB0h7JFDXHGzXoYPsH/KaJor3BAAA)

```kql

//calculate the spatial representation of
//events recorded across time, looking at fine-grain
//dimensionality.  View the scatterchart.
let events = datatable(tickCount:long) [
259310517248,28829712296732160,257802790462,259415631420,
259417595964,27127685174421094,27127590786985062,534293931622,
259416013824,534293536864,3947272620882944,6782045822389260,
439804640768,851673153924341805,122681509722
] | serialize | extend dimension=row_number();
let tickRange=toscalar(events| summarize mn=min(tickCount),mx=max(tickCount)
| extend n=strcat(tohex(mx),tohex(mn)) | project n);
let dimensions = range d from 0 to 63 step 1 | extend eigenvector=1;
let axisNames = range i from 0 to strlen(tickRange) step 1
| extend axis= substring(tickRange,i,1)
| extend dimension = tolong(strcat("0x",axis)) ;
axisNames | join kind = inner events on dimension
| order by i asc | extend eigenvector=1
| join kind=inner dimensions on eigenvector
| extend S = binary_shift_left(1,d)
| extend H =binary_and(tickCount,S)
| where H!=0 | extend pi = i % 13
| extend arc = case (i>= 13,0,1)
| extend euler = (pi*10) +  8- (d % 8)
| extend magnitude =(arc*10)+ (d / 8)
| extend strangeness = tostring(i % 10)
| project euler,magnitude,strangeness
| render scatterchart with (legend=hidden )
```