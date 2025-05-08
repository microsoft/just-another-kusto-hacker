[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHVR2U7DMBB8z1fsC4otYgsqeEJF4r7vm6pKTeKCRWJHtkNb1I9nnRSVIoiVRLs7MzveLaSH0lgnoTsYDCLOGAPOw8uBYQgM/5hrMhzwMB4x/gMUylFbDOiAD6UARMWNqLJKexgZm0MX5NhbkflUFAWJSQ+B/WUaJ60FGk2h/GByXAmdw0j5t1R5WSqdy3F3pBqNFiKqqpj8RjgFDlu4qlCeBGwCMcQUvAE/qaQZEufRyysFo4FEgA/akdhKBJq0SrpU5DmptcpMLtPwqQy6d+nQmjJt6cTRBNjaOm0Upj81hLVigjSdCU/yiRalykhvtY8E8QuuEe6DNpk1VsoSkcAiax5hy06f0h7D/KJSFszXLzNz8e3e2fnW0cXBye7D9d0N51fPTzuP28eX/JTv3x/iqDWurJPA6h8yaogzUrAJK2AsjheWoBOiBK0WZiQtydBU9s10dVkKqz7l93bRA948bcZASvEu00I535DiuGWFHc95pvZV7f9nBl3arjH6AkdRYWmqAgAA)

```kql
let morse =```
.--- ..- ... -
.- -. --- - .... . .-.
-.- ..- ... - ---
.... .- -.-. -.- . .-.```;
print word = extract_all('([.- ]+)', morse)
| mv-expand with_itemindex=wi word
| mv-apply with_itemindex=si s = split(word, ' ') to typeof(string) on (
    extend a = series_add(unicode_codepoints_from_string(s), -45)
    | extend a = array_concat(dynamic([1]), a)
    | extend n = toint(series_iir(a, dynamic([1]), dynamic([1, -2]))[-1])
    | extend c = substring('TEMNAIOGKDWRUS..QZYCXBJP.L.FVH', n - 2, 1)
    | extend c = iff(si > 0 or wi % 2 > 0, tolower(c), c)
    | summarize word = strcat_array(make_list(c), '')
    )
| summarize output = strcat_array(make_list(word), ' ')

```