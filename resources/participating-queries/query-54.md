[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAFWTXW7UQAzH3/cU1gpEi1Kp21I+ihBC4qVUvQBVVXkn3mTIZCaMnaZb8cAhOCEnwZ5ZhHja2fjnr7/tQAKfURA+QKs/gttAcHTVXvooDVzT/pIl+9gdr25XG2hg/SX5qP8LDYuXHnYBfQaMLfBE1K6b1ZmBc3TpgcwXJhShHBlmpswQK3VuFM/jiNk/EUim2HIN6QKpK/DgQ1DylZHiRzpRf08MI3beNbUG6bNSrNiFYc/08doe2HWZOhTFuceJ2hp6orwjJ+Awk6JvDI3Eovbvc43eJSt66akQb41I0lvlE2oH8PvnL1gItim0Ya+0Qu9KhXMu0rgeE4MKmFSbtKh5c2r2XjUKBoTUMQQ/EGCW3Rxgyokt16ZITOh6NUfVhEKotaCAFxhiWqzTTVE4EwZNw77rRZsUDQaak/uas+j73F5Fv+uZ1bj4J8wqs8bTlsCl0uPmok5MMHYl4Ug6dcdNKbUpwx0PaBGXiap/0KimjEujdhP8Q2GKqlo8WZy9FdVTmLQdHLkMrGJVWp30g6fFDFrViIOF1iLY1gCzgUXel7ZZByHdoEk/wg3ut3Ue21mAfXR1ZmdFR4wY9qJtgGdIc4YOx2It6rnUUk2pSXQ3URVURUdrPx7AIuHg3VDErWvP/TaZhA247Hkq2kRCMb4IrasbIU18aHdHFIpW2wNUtM5zPKyAC8kNS8pD6cNhfCGK/qXv3q/sPFc/gB5FDwSuxklvledtvcsjPdEGThvYHP/HnCnkkOnI+BHF9brYeg/0COvbTydf8eTpbt0YqcXA2pz/naJ+PVd/G8V98CwW5MwQ3dNvdjw3xIwdWSGSHco95ox7w8413Pr4D7TLNYhWBAAA)

```kql
let Data = datatable (Id:int, Key:string)
[
1 , "Joining data with flair and speed",
2 , "uncovering patterns users need",
3 , "summarize trends with clever skill",
4 , "time-series magic, data thrills",
5 , "$",
6 , "aggregates shaped with perfect care",
7 , "nested queries going where",
8 , "others pause — we boldly go",
9 , "turning chaos into flow",
10 , "handling logs like artful prose",
11 , "each line telling what it knows",
12 , "real insights start to show",
13 , "%",
14 , "Kusto wizards at the core",
15 , "untangling metrics, logs, and more",
16 , "see the clusters come alive",
17 , "telemetry to help teams thrive",
18 , "overviews that make things clear",
19 , "*",
20 , "hackers? Maybe — but sincere",
21 , "analytics is our game",
22 , "code that earns a streaming name",
23 , "kickstarting dashboards, crisp and neat",
24 , "even ops teams feel the beat",
25 , "runs like clockwork — can't be beat",
];
Data
| extend Imp = substring(Key, 0, 1)
| extend Imp2 = case(Imp matches regex "[A-Za-z]", Imp, " ")
| summarize Imp3 = make_list(Imp2)
| project Message = strcat_array(Imp3, "")
```