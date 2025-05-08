[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA3WRUW%2FTMBDH3%2FMpLCERe8qcON26dpMZPAIve%2BCtlMhNrompk1i2u7YTH55rl7UBgfzku9%2Bd%2F%2FrZQCCfqsqB9%2BBlpQKelQE61O59cLqrGYkWcT7nYjbjEy4md3FCorgJwfr7NFUbxVuffvmq4iSKxXzG5xnPeS7mx%2FsbtdKBm0NaQvOIT3ndd7qSIp9M78Q%2FsE3Xv%2Fumg4E%2Fe13Ny75Nx8WwbVfGncrOh%2B3jTlehkSLL3jeg6ybgG9mRzzPBp%2Fw250K8xhfTjJ9OvHyIDHqwKjReht6XyihHz1rIL2Jd%2FxNKRKRVzkOxdeatz7Dtt22rnH4BYmSrNlAY7QO1%2FAk3stG4l%2BizVIHGBCM4sEaVUDioYU%2Fx3ZNraljyMV78%2BL4jS4TimI03wD44VYZCGUNjyhkSnrGH6Bw2urCm7%2BrPT0NibZ9vzpER2jXgYEDIB5JhCXdDV5F%2BvfYQvHSqq4FmST5Lbo4T7fM17K06EnJgSOhJOFjo11R3YXrChi0WRR63U9vvaJ6QfHbds1F%2FL%2FE3lTsUuJC%2BxkiIvRK3jKTEXriykad%2FWeyX0Vg01i%2Bmy4ZFY8sosi1wGj1f%2FV80TiXkL9W%2FAa9QQasQAwAA)

```kql
let Addresses=datatable(Address:string) 
['29.188.3.137', 
'https://aka.ms/JKa',
'198.90.2.219',
'https://bit.ly/ceh?sessionid=123671',
'https://bit.ly/kno#Title',
'https://bing.com/',
'https://tumblr.com/rstu?width=100&height=120',
'201.6.52.117', 
'160.0.0.0'];
let paths=toscalar(Addresses | project p=parse_url(Address) | summarize l=make_list(p.Path) | project s=strcat(' ', replace_regex(tostring(l),@'[^\w ]', '')) | project extract_all('(.)', s));
Addresses
| project longIP=parse_ipv4(Address)
| where longIP > 0
| extend offsets=range(0,28,4)
| mv-expand o=offsets to typeof(int64)
| extend p=tolong(pow(2, 28-o))
| extend x=binary_and(longIP, p*15) / p
| extend ch=paths[x]
| summarize ch=make_list(ch)
| project s=trim_end(' *', replace_regex(tostring(ch), @'[^\w ]', ''))
```