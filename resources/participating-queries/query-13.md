[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAE1QUW6DMAz95xTeV0Bq4H8TF9jUE0xTZcDraCFBSZi6qYffc2BSE9l+eX6OLU+SKAV2sfeDUEsDJ9xukpKfYwqjO9OBun9YvRs2B1NbuB5ma1sjiHKwL404CK9ZZlV43YTwb7CnDbpMwnkFWRdyiXJx+wc+aRa2ZkYRmQOZxny8FAtGSsQYOnci5GE1WWoI0AKBzVxNuCAa0vYPSlU0u0JLtEiTqjbFXW5J3EAdesRlGlPJaE6mKu40f1u5LaxZvJbgL9JjlX7bVNmp5uJHR9fRDe0kn8mvScLDsr3LpXGdZw7jr9BRYuSztDNf5TSNEe30l32IPaujpNBzOnEI/FPuNOYy1R87p55UzQEAAA==)

```kql
let transcode = datatable(a:string , b:string )['a','.-','c','-.-.','e','.','h','....','J','.---','k','-.-','K','!-.-','n','-.','o','---','r','.-.','s','...','t','-','u','..-',' ', '/'];
print a = '.--- ..- ... - / .- -. --- - .... . .-. / !-.- ..- ... - --- / .... .- -.-. -.- . .-.'
|extend b = split(a, ' ')
| mv-expand b
| project tostring(b)
| join kind=leftouter transcode on b
| summarize Message=make_list(a)
| extend Message = strcat_array(Message, '')
```