[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA02QW2vbQBCF3%2FMrDoJiCfTgFL8VQ4lDCOmdGPJgmzBajbRbrXbF7ArHpj%2B%2B4ya0fTvM5Xwzx3NGhzWK%2ByhB9c2cM0vnT3icSCQecSvUx3CpfDt63M5mwMYZagl3TvhS%2FxLN4ELfOGlx48kMf9SWJeDO06itiA1J6wJ5BZzPqvFEaVKHYCwej1HaTM5jY50ZqGXGU4ztxGZgwdbKnCy%2Bz13nAr663mZLx0EdpPHa%2F0wy4Mes%2B8WHK6HQMxw6iSOWyBHvV0iZJ1xf%2FQK%2FZA4t7JqaVFpKtswxZdELyzR5l8uuRoGi2rlDVVXvVkvd%2BRmVqv%2B1a89djrPGg%2FIVY%2F%2FDrJZvGPzFGM01zc0boNhaxidVcAkjtTWyFh44XQwJXoM9oYvRFzVsjeuqQgyweoGmoyPNSd%2BiZNQ%2FzeNI4s4M4UkD52fhnl%2F%2BPTPSwM%2FepVyaqqrxcbHb7%2FbFvt4fDosai0X1G%2FKxL973AQAA)

```kql
let f = "Hornet Butterfly Sparrow Dragonfly Owl Duck Cicada Firefly Mockingbird Blackbird Tern Flamingo Cardinal Buzzard Wasp Finch Swordtail Chickadee Woodpecker Thrush Puffin Nighthawk Warbler Lark Quail";
range i from 0 to 24 step 1
| extend h=abs(hash(tostring(split(f, " ")[i])))%40
| join kind=leftouter (range h from 0 to 40 step 1 | extend c = substring("The King is mad, the Jester a lucky fool", h, 1)) on h
| order by i asc | summarize replace_regex(tostring(make_list(c)), @'[\[\"\,\]]', '')
```