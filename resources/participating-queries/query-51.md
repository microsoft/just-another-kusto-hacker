[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEANWV0WrbMBSG7/0UQlcyqNAkENhKr7pRBoXe7C4Eo9hKqsSWPPl4Scpu9yZ7s73Ifid27abpSpJlUOwPG/k//zmShU6qialJzK5ZsrYqM7EYccUln4AYJECDKZiBB2DAHCxACjJggQM5+AY8KACBEnwHS7ACa/AIGB+HV0GKCnLlqYcaCvKxIlGUE7wZOxM8U36hYcYGkvXCjrxfyVvd0tW6fqVrZYPnskx13K6CRBGuSaqZMB/ZVhQGo4D//vnrLzeXbynevE+yODX/P6j/VdPDvA+u5JxT3/Pt+HTnXOOzZ35fu/O/L/W+rX7srzlhhwXj4AfTK9I2YbErLUU47DYvbirI1WeeCeWm2JBd9Fr9nSbSvkAATv/dYYwaMxWN5zXjHzhznnUGepdckivzXHtRe422n8eh3B1o/T+vdFySju59on00HCITuabzbMMqdVFmOPjNo2Y3zqIjaAuSrzB5ahKR8l6tRXWgR6kpSOxah5Jx3kl9q90XO3Vtl2nK3zQfqDftYvvod+L2VZCnhtoV3lWEss7Vnfgnr2bOdrPX0S/DR5dYQ3KpW6K6xqryyr2b65gu1FKtX9Qlmxn+AYcgOoPTBwAA)

```kql
let abc = dynamic(["a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"," "]);
let part1 = strcat(substring("marker", 3, 1));
let part2 = substring("worker", 2, 1);
let part3 = substring("maker", 3, 1);
datatable (i: string)
[
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤ",
"ㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤ",
"ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ"
]
| extend count_ = countof(tostring(i),"ㅤ") -1
| extend Letters = abc
| extend Letter = iif(count_ == "9" or count_ == "10",toupper(Letters[count_]),Letters[count_])
| extend Execute_Order_66 = todynamic(Letter)
| summarize ConcatenatedText = strcat_array(make_list(Execute_Order_66), "")
| extend GeoInfo = strcat(toupper(part1), part3, part2)
| extend ConcatenatedText = split(tostring(ConcatenatedText),GeoInfo)
| extend EDragon = strcat(tostring((ConcatenatedText)[0]),tolower(GeoInfo))
| project-away ConcatenatedText, GeoInfo
```