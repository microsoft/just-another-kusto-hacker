[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG2RzUoDMRSF185TXGYzGZiiVhFddOHCn5X4g0IpZUgnlxI6SWqSKbb0EQRBcO1TCL6VfQSTOJ3W0azCzXfOufdmqrm0gLJQDNmp1nQOPWBzSQUvyCDaicd3+1eXrDxDK7G67vXizBWrkwumHkSxKd/0w8M9W9wejJqyCcVuX2+x6jyOhmm0BDHr0Om0nMOkMla52F9dKAkkAnfwyaJkwNBiYfkMHWisLlGSoEsDtFxjdOxc/AxWucHIRrUL3RYqKKvNCmqJqUbuxuX4xzbbCuzUrmkGf6i9f8EUWlE+SOMMtUHic9sAZYwXFpnvp4kQmEE3W08rnKgDx60hwuJG1ODRYc7Q7y+3qtavTdthg2TyWCbDrZYGiVXJsOFMJQTVfIEOXb2/PgdW0AnmJTeWOHUa+R9s/Fbvbx9fny+Bo/778nqrjT6DGOL0G5lExgtuAgAA)

```kql
print encodedArray = dynamic([
	"gS1NHdlEetneuP==",
	"u9GdoVmclEetneuP==QY",
	"UdzR3blEetneuP=s",
	"2YrVmclEetneuPoF"
])
| mv-apply kusto = encodedArray on (
    extend detective = strlen(kusto)
    | extend agency = toint(detective / 2)
    | extend made = strcat(substring(kusto, detective - agency), substring(kusto, 0, detective - agency)) 
    | extend me = reverse(made) 
    | extend addicted = substring(me, 2, strlen(me) - 8)
    | extend to = base64_decode_tostring(addicted) 
    | extend ['kql'] = reverse(['to']) 
    | summarize ['💌'] = make_list(kql)
)
| extend ['🕵️'] = array_strcat(['💌'] , " ")
```