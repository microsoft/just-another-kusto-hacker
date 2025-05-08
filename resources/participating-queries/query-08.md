[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI2OP0vDUBTF93yKywMhT1KwmURxCCFDKVIwOJUSnu1TgvlTkteQiIOzDt63WEfBoYPoJAgq+GHuFzGvqZugy+Xcc889/BKpIG2UOEkkwAHMhBLrxa76e6Uq4uzMgcrdSG6NGel30ivSS9KfhEj6mfQL4dN6vSe8IbwjfCB9S7gk1KRfTaZ12qv+IHwk/CJ8I33NHIsN/MA/CrxDfzQaDoLQ94ZBGHrHfsAm+9YGzLoEWSuZzaBuERdZPM1nMjJjnseZKqPTIk+jDrHl5g40/8i5HNritOrJei5Mt9MYo1ykqSjiCwmiKERj4lOh7FScyyiJS2X/0qvyn1ZlDLuGXif+YGCEV4yPdyacwzZ0Lw2HLei7u5w7jPFvz/VKDJ8BAAA=)

```kql
let mytable  = datatable(v1:string, v2:string)
["㑺㑧㑗㑼㐐㑭㑮㐫㑼㐘㐋㐖㐠㑏㐗㐑㑴㑭㐠㐘㑻㐣㐿㐷㑊",
"ICECREAMCOOKIESCAKESSAUCE"];
mytable
| extend x = unicode_codepoints_from_string(v1), y = unicode_codepoints_from_string(v2) 
| mv-expand x,y 
| summarize array_strcat(make_list(unicode_codepoints_to_string(toint(x -toint(unicode_codepoints_from_string("㐀")[0])) * toint(y) % 128)),"")
```