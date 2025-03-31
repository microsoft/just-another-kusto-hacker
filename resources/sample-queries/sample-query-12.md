[Click to run](https://dataexplorer.azure.com/clusters/help/databases/ContosoSales?query=H4sIAAAAAAAAA02PUUvDQAzH3wf7DnEP6x0e4rY3peAe5qajCKUg0pZy1NiN3l3HXQ6K%2BOHNFKYPISH55Z9%2FDBLYBaSQvPQKXtG0g0UoBnhe73eco3faoqNwldxPJ%2BZML8%2F0Gwa1021%2FdB3sY6ABnsLdNt%2Bsi%2Fn8Mbo%2FenWmc4quUNv1IW40KJdv40H1RYebC5aS1y4YTSjsUrEljpXkKbc7hBE%2B%2FGDhFvhQIG%2FQCSu5whMsp5MvwJHQvUOWcuF1S402RiTiRiasI%2F8ROYZoiD2xSqtJZKUYrxeyVlk51j9giNZqf%2FxEyDAE3WHq8WR0i43HDkdBA6%2Fy28LqHhtzDCR%2BRaVUD0lZldWsUlVdJ2o2k9%2BKlixHXwEAAA%3D%3D)

```
let m1 = 'Ok, Welcome To JAKH Tournaments!';
let m2 = 'Yes,Hacking Kusto Is:GREAT&&Fun!';
let m3 = 'RtunT,GAhuEa ,nRGuh,kTgeE';
let m=translate(m2, m1, m3);
range x from 0 to strlen(m) step 2
| extend M=extract_all('(.)', m)
| extend Result = strcat(M[(x+1)],M[x])
| summarize Message=replace_regex(tostring(make_list(Result)),@'[\[\"\,\]]',"")
```