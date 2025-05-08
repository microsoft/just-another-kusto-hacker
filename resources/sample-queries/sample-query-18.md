[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA52RPWvDMBRF9%2F4K4cUyVSD%2BaLdAIEM62EtDhxIHI8uvton8gaQmsumPr%2BShaGhC6WAw3KN3j55G0fYKoSxEG%2BRXO81Zq9flpCf%2F4QuBVtBXKItsyCa9pjs9p3vF3TBeTh70JX15k%2B%2FXzcYNExseWt2UrU7TfdM4IbedJZXwnBQVsKGCQg1SGaEaZ2FAEI%2FuAJEF4jtAbIHkDpAEjqh1Mf%2BCMlVQzvHWw%2Fn1MfDMDKuyrOBGbk2WLdzIrciyiBt5EiBH5MmAI2XnggpBJ%2Bwhjzifi86GnNvR7IpkEcli20KyJ%2BdWr4YQtK8Brwla5hUc%2Blo1eA5WIUGhZbvLCvRI7UBiTqgBqWmE4QPzoa8tMIgKBConE1YgmTWQn11HRTsDmqXp6OgZCt5KZeb%2BqV3%2BWi%2F%2F0Z%2BBlLQGWwUjpwwKATVo%2FPPMjpsMzEts%2FWN%2BzL2c5KeTT5DvB99VP2CCAwMAAA%3D%3D)

```kql
print  M1 = 'dCxlcix0byxy'
| extend M2 = 'cyx0aCxzLGtl'
| extend M3 = 'dSxvLHUsYw=='
| extend M4 = 'SixhbixLLGhh'
| extend l1 = base64_decode_tostring(M1), l2 = base64_decode_tostring(M2), l3 = base64_decode_tostring(M3), l4 = base64_decode_tostring(M4)
| extend M1 = extract_all(@"(\w+)", l1), M2 = extract_all(@"(\w+)", l2), M3 = extract_all(@"(\w+)", l3), M4 = extract_all(@"(\w+)", l4) 
| extend M5 = pack_array(" "," "," "," ") 
| extend z = zip(M1,M2,M3, M4,M5)
| extend R = range(0, array_length(z)-1, 1)
| mv-expand z, R to typeof(long)
| order by R desc 
| summarize zs = make_list(z)
| extend R = range(0, array_length(zs)-1, 1)
| mv-expand zs, R to typeof(long)
| order by R desc 
| summarize Message = replace_regex(tostring(make_list(zs)), @'[\[\"\,\]]', '')
```