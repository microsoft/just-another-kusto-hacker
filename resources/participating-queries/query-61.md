[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAGVUTY/bNhC9+1dMdVkZULuS/M0g6CFAWnd7SJEFcggCY0SObGYlUiCpdZSkQP9D/2F/SUeSvbZb62Bo5s2894ZD3d/DL44oaLP3CTy0Plh4i8b/MLm/h1/xmaCzLdAzOTiiCaSAAcExorSuBlt42TqC7bvnJaBSjrwnD9owypN0FOBoneLWfT9pzece7RuUjLJtAFtCOGgDqF0CaFRPZYAq2jNb1QFWganDgUCiZ5HAtCDJBeSiuvOc1bb13Lo1wWnyP/dEH6iqEijoYCs1FB/1V3TKdRyr7HEw90EHw2r7tO8NXMmXtib2uSfOud7w8aB9c9Jx0EqxxObgkOv++etv1lhBY4/keDpFN4Baw4NsGiwqghr3WvZGH/74fVLxRB4PjjBseZpVpfdkJMFrUBj4YXzcz1J4NmP2048T4F+Up2km8mUqhFyvoiTKMc1FmUkO5Gq16CMDYs2BzeICITXnCC5IRcnYqaQek1GRi3NoKJ1x83macm6sRbEuuRbP73Mh5+dsjy+LVGTpcnHO5wKL9Skv01KUcr0RtBBFVojsAlpsKBWpWLGE/EWSUoWYbWYrcStpPivXzHHhVGUmSL5InIl1cS1JkRLyysJMZBmmI/vYlllvGFTJDheXDtlMrsQyTYtrzpxpLqRLsZm/vHDzJV2ZpmK55rdPr8Zj3r5D53lrXkP8uBU35zr9Nsh43A5/34G+BOLlf29bJ+nNsMsd1+3J7rQp7a50tt7pZnfa0aHX9Kdx6btTj8bZzyTDj09EzW2nyZ+vJv9fusl3vqfP9olelMbTyUVKQBcG8b4tRtXxTdME0gSyq4qPd2/1F3gzXNO7T1zIN5biQdytL23i6Dds0PDcHsh0GE2TM994PNpT3YTulpBB0e50fsFW/YWLT1XTXsbZPx6xg/9IPeEY5du6Rqe/Erwfv09sMDiJYYfOYRfX+ES7SvsQ3/qZJlF0PZ5zsaOm4q/Z7jyiIT4qhTu4m8K/thOBAGIFAAA=)

```kql
// Greetings, Kusto Fans!
// Have you ever wanted to transform obscure IPv6 addresses into secret words, 
// conjure spaces out of thin air, and even elegantly alter the casing for certain mysterious countries?
// Well, behold the wizardry below!
// Witness these IP addresses come together to whisper the hidden phrase – all powered by the unstoppable magic of KQL
let ThreatIntelligence = datatable(IPv6:string)[
    "2001:260::c87","2a02:f1c0::2d75","2001:280::9587","2a02:ed40::a5ed",
    "fe80::1eb2:",
    "2001:360:4000::","2a0a:8f40:a::","2a04:c400::","2001:fb0:1065::","2a02:ab80::","2c0f:fc89:e5:b1b:1::","2a02:59e0:0:7::12",
    "fddb:3937::",
    "2001:43f8:10::","2001:df1:ec0::","2a03:8b00::","2001:ded:c000::","2a03:11a0:1::",
    "::1",
    "2001:df0:a5::","2001:13c7:600b::","2001:df2:8bc0::","2a06:940::","2a00:16e0::","2c0f:eb68::"];
let TIParser = (TI:(IPv6:string)){
    TI
    | extend SourceCountry = geo_info_from_ip_address(IPv6).country
    | project-keep SourceCountry
};
ThreatIntelligence
| invoke TIParser()
| extend Starter = substring(SourceCountry, 0, 1)
| extend ['Fix Casing'] = case(
    SourceCountry in("Japan","Kenya"), Starter,
    isempty(SourceCountry), "_",
    tolower(Starter))
| project-away SourceCountry, Starter
| summarize Secret = strcat_array(make_list(['Fix Casing']),"")
| extend Secret = replace_string(Secret, "_", ' ') 
```