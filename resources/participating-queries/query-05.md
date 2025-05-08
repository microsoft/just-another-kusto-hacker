[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH2PzUoDMRDH732K3JrVLbRLqRXJI/gEImHYjmvq5oMklSoeWkUoCAp+XPSgj9hHcFayshTx8M8vM5mZ/6TGyKSG87k1FROsv/1crUnvpFvSW+JL4itpRfpK8TrxMfGpU9dwk3if+Nzpb3o//vFp53X9Nju+d4kPuz79o57zykS2MKq0M5TN4SxlgjzzVssQ6bni7d+z3g1z3s6xjAwEeA9XMrhaRf4zRg5zD6ZCXuTjaV5kTbm+HODSgZkxoAiXEelaCg4nw9PBqJgcHkyyvfF0nxKj3wRVhoXW4NU1Mis0XKCsVYi87G5wjCFAheKv7aNtd7fZN2/wlQS+AQAA)

```kql
let _mahjong = '🀁🀚🀂🀕🀂🀓🀂🀔🀀🀠🀂🀁🀂🀎🀂🀏🀂🀔🀂🀈🀂🀅🀂🀒🀀🀠🀁🀛🀂🀕🀂🀓🀂🀔🀂🀏🀀🀠🀂🀈🀂🀁🀂🀃🀂🀋🀂🀅🀂🀒';
print unicode_codepoints_from_string(_mahjong)
| project a=array_split(print_0,range(2,48,2))
| mv-expand a
| extend c=(a[0]-126976)*48+(a[1]-126976)
| summarize o=make_list(c)
| project Message= unicode_codepoints_to_string(o)
```