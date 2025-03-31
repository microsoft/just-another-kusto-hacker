[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA33STWrDQAyG4X1PMTvJ0IUl%2Fzf0Agk5hDGuWxqSYk9WoXePkkWiMeTzyuBnBqxXhzGGr1zCZ%2BDhY4nzz3HKwsVehj7y8B5uD82U%2FW%2FeDneqL6ldwzRS9rQFsMr0620JbME0eFsBWzL13tbAVkzf3jbA1kzB2xbYhunkbQdsyxSdlRzYjmnx9nU2u4fp7C3oJtZt5y3oJprOQUA3sW6zt6CblOnuCOgmq24Cukm9mi%2FoJqtuArqJdTs6q6CbdOlOKuimeTpfBd1U0n9T0E013R0F3bR47M6ffY1hPy5LP412ws4xbSnbXAEAQRioOAQAAA%3D%3D)

```
let f01 = (c:string) {strcat(c,     'r')};
let f02 = (c:string) {strcat(c, f01('e'))};
let f03 = (c:string) {strcat(c, f02('k'))};
let f04 = (c:string) {strcat(c, f03('c'))};
let f05 = (c:string) {strcat(c, f04('a'))};
let f06 = (c:string) {strcat(c, f05('h'))};
let f07 = (c:string) {strcat(c, f06(' '))};
let f08 = (c:string) {strcat(c, f07('o'))};
let f09 = (c:string) {strcat(c, f08('t'))};
let f10 = (c:string) {strcat(c, f09('s'))};
let f11 = (c:string) {strcat(c, f10('u'))};
let f12 = (c:string) {strcat(c, f11('K'))};
let f13 = (c:string) {strcat(c, f12(' '))};
let f14 = (c:string) {strcat(c, f13('r'))};
let f15 = (c:string) {strcat(c, f14('e'))};
let f16 = (c:string) {strcat(c, f15('h'))};
let f17 = (c:string) {strcat(c, f16('t'))};
let f18 = (c:string) {strcat(c, f17('o'))};
let f19 = (c:string) {strcat(c, f18('n'))};
let f20 = (c:string) {strcat(c, f19('a'))};
let f21 = (c:string) {strcat(c, f20(' '))};
let f22 = (c:string) {strcat(c, f21('t'))};
let f23 = (c:string) {strcat(c, f22('s'))};
let f24 = (c:string) {strcat(c, f23('u'))};
print Message = f24('J');
```