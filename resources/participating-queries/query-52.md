[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAIVTW2+CMBR+91c0zR7ahCWbuzxs8YG32fbF+OQ2Qyo0hAzUIBs69b/vlGsL6BCwnHO+y+klVhliXDDOppwxITiaIFJ8C/6yy9JoHTrlJ1TVAaQjAp66hB6zTTkiap+l0s88GcekAToNgNLz6yjuiLILoqK4GH8JDmuZRL4hY6aHKMWlPhiYgKARGwjBPAgrSI+p2sbSV16qQrUnJpXJYYP7xuAaMMYsRaPZakjYZVZxhZUX09NSOrqYtz3Bvy9hqdJUHkhbXpX1dUB9QEdoU2WsYV7JnXp+9ALlbwLlNatmlNbsFTfc8BvuQmdYVWRsuGidkU62tcysHV3P4we+wQ6eTOAF9/gJL+nraAuERZeiZNMGtRE8D4OZnwfu1F3MVuEKRtJ9n/nh1J3nZWaVTyG2mC1ymesMpqMTghOg1gGquDSVdcAILqQYBwfk8zM/js8UO7Y8RSeU/Nyq/VYCk7V9DHitoEV330ki0+hXIebyt0ZTdED9F3YS+aW8ONrBbJorPYwpnLan7CqxdcR7lYb/bqWGGgv4cbf8t+R+SSl1rM1EcD0s93MX8gCQvscKr3GwIF3MGDCjP+fISbE0BQAA)

```kql
let JKLJKJIKJJLLK = (KLJKJLK:string,KLJKJLJKL:string, KLJKLLJKK:string){tostring(extract_all(KLJKJLJKL,KLJKLLJKK))};
let JKLJKJIKJJLLJ = (KLJKJLK:string,KLJKLLLLLLJK:dynamic){tostring(KLJKLLLLLLJK)};
let JKLJKJIKJJLLL = (KLJKJLK:string,KLJKJJJKKKJL:string,KLJJJJKKKJL:string,KLJLLKLJKKKJL:string){replace_regex(KLJKJJJKKKJL,KLJJJJKKKJL,KLJLLKLJKKKJL)};
let JKLJKJIKJJJJJ = (KLJKJLK:string,JLJLLKLJKKKJL:dynamic){todynamic(JLJLLKLJKKKJL)};
let JKLJKJLKJJJJJ = (KLJKJLK:string,JLKLLLJKJL:dynamic,LKJJKL:string){strcat_array(JLKLLLJKJL,LKJJKL)};
let JKLJKJLKJJKKJ = (KLJKJLK:string,LKKJLKLJKJL:string){base64_decode_tostring(LKKJLKLJKJL)};
let LJKJLKJLKJKJK = (KLJKJLK:string,JLKJKJKJJLKJLKJ:string){toint(JLKJKJKJJLKJLKJ)};
let JKJJKJIKJJLLK = dynamic(["$","==","","25"]);
print JKLLJLKJKJLKLJ = ("SgdQcwdAIAYQbgbwdAaAZQcgIASwdQcwdAbwIAaAYQYwawZQcg")
| extend LKJKJLKJ = JKLJKJIKJJLLK("JKLLJJK","(\\w{2})",JKLLJLKJKJLKLJ) | mv-expand JKLJKJIKJJJJJ("JKLLJJK",LKJKJLKJ)
| summarize JAKH = JKLJKJLKJJJJJ("JKLLJJKLLJJKLLJJKLLJJKLLJ",make_list(JKLJKJLKJJKKJ("JKLLJJKLLJJKLLJJKLLJ",JKLJKJIKJJLLL("JKLLJJKLLJJKLLJJKLLJJKLLJ",JKLJKJIKJJLLJ("JKLLJJKLLJJKLLJ",LKJKJLKJ),JKLJKJIKJJLLJ("",JKJJKJIKJJLLK[0]),JKLJKJIKJJLLJ("",JKJJKJIKJJLLK[1]))),LJKJLKJLKJKJK("LKJLKJKJLKJJKL",JKJJKJIKJJLLK[3])),JKLJKJIKJJLLJ("JKJLKJLKJLKJKLJL",JKJJKJIKJJLLK[2]))

```