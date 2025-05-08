[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHVQ0U7DMAx831f4LYk0ULcxtgnxA/AJCFVearasaRIlHmoRH4+rVgiEePCDfXf2nT0xnKmHR+BYLHrMOmUXGJyMMoYT6WoJq62UWXxC936DKflBYI7AQ6L4pn0MJwMxgKaeKTQCyUrtzKgo167D7D4IMGcc6sLZIusOW6q9Kyy0JShlzMPCixcpplzkuOzKaLlG77XSt0YtFVo6P7XPIebCV1AimbxesJ0yqDuLx6ba7Y+b9aG5l2bfbKrVdn1QYiXleCH7g/73xIzNUalPKHGmmYzmeGMv6tnqiwsN9fIG4XzrX38lnwX/PGBEpx98AQ3+QMqNAQAA)

```kql
let hex = toscalar(print i = range(0, 15, 1)
| mv-apply i to typeof(long) on (extend tohex(i))
| summarize array_strcat(make_list(i), ''));
let letters = extract_all('(.)','acehJkKnorstu ');
print jakhex = '4cabd078b329d6cab8d301529'
| project jakhex = extract_all('(.)', jakhex)
| mv-expand jakhex
| extend jakh = letters[indexof(hex, jakhex)]
| summarize jakh = array_strcat(make_list(jakh), '')
```