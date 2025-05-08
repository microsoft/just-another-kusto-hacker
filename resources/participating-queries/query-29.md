[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAFWQzU7EIBCA7/sUpIlJN6kToH+7MT15MF7U7As02KWKtqUBqq7x4R2g6pr2MMx88zHMIB1R07y4hiSM5lACKyiwjOwgfBgwKEqIuRL2VQzZnvsAGM/xgAyN+YJBuVtpDqzeQVUEnmEOw1gpgP/i+RruS+BrnfH6zMcpGqpYoDxYGKfAy9KTDOr1Po7j18W/u2seu4It535sCvv1wh0NnhBX+JJ8fWWFTeWaR9y3RL764ZOrzWzU5Mjtg23C9jZfZDb6RXaO2HlQLsVKRhL8t1ga3y7lxyymIzaQxncRp4k7zVL3qXWoevKY/HASmRupEXqSulVTr9ve6LFVcyuORyOtRfMZS66fhUG602KQtpOpXR6jMEUNdHqZnDllNGPbLInDWGmUGNSnJH+aw11j9Hs7LeOjNOmZf9Wrvk8Pd+SCsJw0DcFl+EKGrxj0O3b40zbIl3EUxst9ymLrKF5lOyjrInS2qPvF4eYQwYE74VphjDgFymZJsv0GeBO4spoCAAA=)

```kql
let input= "103.5.140.1, 8.8.8.8, 81.45.0.1, 85.96.0.1, 192.0.1.123, 181.0.0.1, 41.58.0.1, 82.178.64.1, 110.164.0.1, 84.2.0.1, 41.32.0.1, 95.24.0.1, 127.0.0.1, 41.204.160.1, 102.164.120.255, 121.78.0.1, 203.74.0.1, 82.178.72.1, 10.0.0.32, 190.92.0.1, 80.120.0.1, 61.135.0.1, 62.150.0.1, 90.190.0.1, 86.120.0.1";
print IPs=input
| project split(IPs, ", ")
| mv-expand IP = IPs to typeof(string)
| extend Geo = geo_info_from_ip_address(IP)
| extend  Char = coalesce(substring(Geo.country,0,1)," ")
| serialize 
| extend RN=row_number()
| extend Char = iff(RN % 13 == 1, Char, tolower(Char))
| summarize Chars = make_list(Char)
| project Output = strcat_array(Chars,"")
```