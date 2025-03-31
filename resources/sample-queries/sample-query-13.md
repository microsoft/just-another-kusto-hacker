[Click to run](https://dataexplorer.azure.com/clusters/help/databases/ContosoSales?query=H4sIAAAAAAAAA33QTUsDMRAG4Lvgf3jJxQ%2F2stZrD95E62kFz8Pu1E2TZspkaiv4451lpepBCSQwk3l4E6XyyjhirbJFCxPfqvHOj4%2Fzsx1pZaRYhqVypiMPCCu2iod9NYz0xqiyZaz3JeAQbcQ15hsBXYsLX174DeEkvcSccRBNoCI2smKg94AZ8sEw9Ry6%2BYL%2BCPTsk4xYUQQzYyIZOSbGo%2BcUnLKFqeji4n%2FRHzBh99Qn1wqTIto3UsSJ2x%2BEyoZ7w0ok3dkTY%2BlfqD3ZZdc2Hr%2FpFs00cPUJZ6bKwW0BAAA%3D)

```
range x from 1 to 1 step 1 |
parse kind=relaxed "Lets Just have some fun" with *  "Lets" S1 ' ' *  |
parse kind= relaxed "Will work another day"  with  * "work" S2 ' ' * |
parse kind=relaxed "There is no other tool like Kusto " with * "like" S3 ' ' * |
parse kind=relaxed "Let no Hacker near it" with * "no" S4 ' ' * |
project LookAtMe = strcat(S1, S2,S3, S4 )
```