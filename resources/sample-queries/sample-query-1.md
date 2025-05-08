[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA11RS2%2FCMAy%2B91dEvdBKMOXVpJ2EtCPaujMHYCgrUQm0aZemG5r24%2BcwNAGOFMv%2B%2FPnZO2M9KtEcxej5RVV6f7SdG%2FwYRz%2Bod91BV3%2BwPnmnKr9VTZNMkod0MkVleh1DIKgEJ71odtH8orOggdB%2BzvSpV3YXKLc2vbPZnc3v7Oyq%2FhLSD95VyiclCW2EFkL5UDo0CgNoIC0gbq%2BGfbJMQ7ZDZyw6GrubG2u1G635GHWURAhkpzy890ajZPHYdLYGRvCvzj9IPOMC05xJkRGZ07ygArN4iv7xnBSs4BkWhaCcSonlNToTVArGiSgIZYwISqm4wXOcUYmLgjLMBYdk%2BJZOMkmF5CRnmDEueS7jM7qJUtRZtID5hrFtlTPfGr3qYVC1hvGd7hu49NbpWp8S38HajK2TVh31tjGDh9WkU%2FQ0Wb2tv9bDBi4dx%2Bkv%2B895MCkCAAA%3D)

```kql
print L = " JKacehknorstu"
| project L = extract_all('(.)', L)
| project L1 = L, L2 = L, L3 = L, L4 = L, L5 = L
| mv-expand L1 
| mv-expand L2 
| mv-expand L3 
| mv-expand L4 
| mv-expand L5
| project W = strcat(L1, L2, L3, L4, L5)
| extend H = hash(W) 
| join kind=innerunique
(
    datatable (H:long) 
    [
       "-4602837651782892603", 
       "819394506962427707", 
       "-6276341691233162226", 
       "-805270992304648190", 
       "-6157267418303347487"
    ]
) on H
| summarize Message = replace_regex(tostring(make_list(W)), @'[^\w\s]', "")
```