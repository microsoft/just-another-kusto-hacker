[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG1RTW+DMAy98yusXgoSqOu52k6rJq3TLjtOOxhwIYUmyDFqmfrj56Rb6WE5xXkffo57Ejhg18IjLF5HL4DWSUsMOy0ctFh1xItN0iuvRE/KY7QNge/MAHt2R3gAJXrhnmwarDItaIB1cgE6C9k6NvgQNrZReShm6HNZtcjLLwX8WPpIii557JDDOlPywO5AlRR4wunObUZuPjmYOngJVyjp/BrMgpMnNtibb7qOZF1NXvlhtAT0XOCk0xMYr/9Ax0GmFKxmTU2dZZsk8m7hVSsq/sOTf8QRC7wsg7u4nisVmjqPHgocsaOiYRzaiBXF09X9ZKT9TemsCpLVike9WNhtdVc1VM7uTTNq1zec3BjyvLAbB1Lv96grFCmpD2OG38jhmaw3MoW16aq19fkH0XPXFQYCAAA=)

```kql
let jakh = "Just another Kusto hacker";
let base = range skip from 0 to strlen(jakh) step 1
| extend jakhString = jakh
| extend ['char'] = substring(jakh, skip, 1)
| project-away jakhString
| project ['char'], id = strcat(['char'], skip)
| serialize;
let nodes = base
    | where isnotempty( next(id));
base
| extend dest = next(id)
| where isnotempty(next(dest)) 
| project src = id, dest
| make-graph src --> dest with nodes on id
//run in KE and configure Layout = Grouped, Nodes - Labels = char, Density to the max
```