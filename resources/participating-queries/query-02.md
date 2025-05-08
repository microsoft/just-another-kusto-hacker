[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAA2OUWrDQAxE/3uKIVCyCxvIprFJAr5Ae4RSjJwo9hJ7HbRy2pQevkIf8xgeki6kNt3ILp8wzrn3+DzsYx1QxSogbg/7gONxZ1hVhnWs6q+XP0yPDf/cKV9QGqHcs4tvAduATfTQGfq883x1Kas3+3tgYXQpkzzbMqSrtpL6QV0OKB6v2KFpEM0syzSRpF8GiZDJKmdSN9GN2zEVdWXprEu5d8IPlsJu/X6+zfhYitoVymtvO+1db7laefwDZRlwBuIAAAA=)

```kql
datatable(n: long) [8416, 515, 1084, 992, 1554, 6156]
| mv-expand s=range(13, 0, -1) to typeof(int)
| where binary_shift_right(n, s) % 2 == 1
| summarize array_strcat(make_list(substring(reverse('Jcko Kustheran'), s, 1)), "") 
```