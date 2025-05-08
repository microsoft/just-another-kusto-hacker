[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEALVUXU/bMBR976+49GWtFEpT6MeYqmkw2GBCm8qkPUwTcpPbNuDEme00ZOLH7147/QhjT9OoRBL7nnPux7GPjuAWEewKAdeYWUOvwkKJGkGq5RJjUBmoQoMtFaiFe53hMqHVy0QiGNRr1KYHtyrFuYorKIWjURCthJSYLREKcwCtIyeVuq05goBZEsfEQJ9GyTXCvKJAEFlMD3RCnwpDu18UpeNgMUYqJk1bLBY9JpyhiCESGheFlJUr42PC8sxixQNV9Wi1gEzZJEJYKA1XWZxEwirKuSXR1sW8e++ppxALS7+5xM4FN+Tq/SkQYwDnusqtOiVxnWTLwOnsvraspzBXSnZbQH/f3f9RAO3REMaDNr3cJFpTEql/UBM55ZL61A4WQhoMHGRMkYM+DPsM+cYDSYyLTJWxEKk0JeTPAnUFUmTLQix9GzEqNL5tUE321U/OYEzvxzA+gdFlO7C6qMNec9g5DLwiwj11HjTmUlDbwj6UiV3BpMEc9hkzgVHImGEfnAyMzvd5w5CDjmF0xkEfNKKlfrlhphX5gRJObAWfc9TC0hwMLHSCWWwOmlqDRhPVmkhAkfGYqGKrZDToepY1svXjzd6Az/7fgLlEKnw85NwulZSqdMNaOSeWCLmmhGPsNUriitwkGHWRGZocV0Ie3RLsWbUBPfb28I2nYV3zsGTygPWp4yM3o7WD/UmccAcv3NhJ7zFXhs8gTUBTj0ry2CsDK5HnmFG9Tb0hp0qOmTD0q2Y1V5+IHlAT7Ji84W6P3rPW+7M4hSLj+6Jx0oLGWFpPlALfOduSYToFTn5HFBKRVSYSUuiOp35qUWvvMbKHD4i5WwugnuqWsv5mwgktbhCiFNVmr7tTGfy7Stj/u8xLnYDnrTBKW74NN5zCRMDLRZoKnfxC8JExpUr2pHbdCa1F1UnpwruTibEd7+UujQvaXYLS4aBDtYerj/adt3en3vCmH/hHyMB0fUieoKu1jrgxS1bNZWJ3IBbhu6zj3PJHmh6zS84qqUjTp95p9x/JVrvQbtefrS7surixac3STJoxuxK3kaaY13F+KYDwxbA6i2tKwi92fwNiLvH3FAcAAA==)

```kql
// See the events that were logged on our two of our Region File servers. Somebody wants to challenge us! 
// Seems to be a Riddle to solve by us and use our Kusto Powers to decode stuff.
// Read carefully the Hints and take extra notice for Indicators.
let RegionADecode = datatable(EventID: int, Crypto: string, Hint: string, Indicator: bool)
    [
    6, "65 72", "Mirror mirror on the wall",false,
    7, "20 50", "What is the most common query language to secure?",false,
    8, "65 72", "4B 75 73 74 6F",true,
    9, "6C 20", "We just replace 10 with 8",false,
    10, "68 61", "50 65 72 6C",true,
    11, "63 6B", "Greetings to my Security Operations friends!",false,
    12, "65 72", "Moving over to your next Region",false
];
let RegionBDecode = datatable(EventID: int, Crypto: string, Hint: string, Indicator: bool)
    [
    1, "72 75", "Follow the hints we provide.",false,
    2, "73 74", "Ensure you follow the Indicators.",false,
    3, "20 61", "We Just like to change Rust!",true,
    4, "6E 6F", "Expose a Secret what's happening.",false,
    5, "74 68", "Trust the hacker's 3th event.",false
];
let Hints = union RegionADecode,RegionBDecode
| where Indicator == true;
let Hint1 = toscalar( Hints|
project-keep Hint, EventID
| where EventID == 8
| project-away EventID);
let Hint2 = toscalar( Hints|
project-keep Hint, EventID
| where EventID == 10
| project-away EventID);
union RegionADecode, RegionBDecode
| sort by EventID asc 
| summarize Decoded = strcat_array(make_list(Crypto), " ")
| extend Decoded = replace_string(Decoded, Hint2, Hint1)
| mv-apply DecodedMsg = split(Decoded, " ") on (
    summarize DecodedMsg = make_list(tolong(strcat("0x", DecodedMsg)))
    ) 
| project Secret = make_string(DecodedMsg)
| extend Secret = substring(Secret, 1)
| extend Secret = strcat("J", Secret)
```