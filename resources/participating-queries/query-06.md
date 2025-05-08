[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAGWQ0W6EIBBF3/0K4hMmthEElW72S5rGoI4NrYjB2Y1r+vFFtg+7aUgmzD0zcwcmQILddB40htNNQLc3M2P2zrhQnDEueU6kKLmsWC1zwpTkSjV1XRwya1iQVZRLUapGNOFelaUqpCzUxykJs5MfAhvCPJCdnMnovNXYmuUq6JYFtl6s1d7sEPGKvtdItff61j4lvZuPxOpvaCezIt2zLCfpaxojYyLNnp3WZTKh6l4TkL2+wLboSNERvC3gRho8zPx58MW7L+gx9qILnxAc/u33aP/Q0+kVKtEO0LsBWnT3qfRPhjnKo3c2vuVYPfkFBmXJMHoBAAA=)

```kql
let tbl=datatable(x:int)[1249211252, 543256175, 1952998770, 541816179, 1953439848, 1633905509];
tbl
| extend z = format_ipv4(x)
| summarize z = strcat(array_strcat(array_concat(make_list(z)), "."), ".114")
| extend z = split(z, ".")
| mv-expand z to typeof(string)
| project z = toint(z)
| summarize z = make_list(z)
| project base64_decode_tostring(base64_encode_fromarray(z))

```