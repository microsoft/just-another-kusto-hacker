[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJWV0W6bMBSG7/MUFlcgsSmEZkjbMmnqbqp26rZW2kUUIQdM4tZgZJslrO277xgMhSYSHjeGw+f//OcYG0YUuv55E9+QI014gVYorQuc08RdzxBcTin4A0mU4+unNiSrPMeC/iU62IYeOC1apKeuK6l4F2tDjKgeMqHDnggypkpBCzUO7XHySIRjQhvv0wyk0FcpSb5ldfyD4VPnTyDufEQLHzkUxjmMGYxOVZZa6qXzbrjAcEHzZnyd4+YTXGi4cIJ7pxOeS3AxMXFhmWBuuMUEd2HJLS0btbTU+2Cpd9Ko8D9XYipBaGnYdmVDy4U8KSyyLCyyLCyyLCyyLCyyLKzjlujlLdZuYoGLHUF3ipQoEzyHghVHWAhcx4wUO7V3R1vcg05JDQezZ0SOihQpuiqkgq0/4tZacfPK/OYivUqPgCnOeLFz9aT3B2+okpLjrfiOBRwzwFGauVQWFWMtSz0flskfzafeQOAeSpEZF3mTRCo4wgyWDahf+HC5xzpBgiVxZ20rOntfVnqvymprpvc6g/N5beANGBqZ9lHg+W8EPzd7Hzld3HHM+gwsnfEzqGXVHZe69ObONTX0ycY04wdDN3cndNeBVx/gFVq+rdvPAMsEYv0PprEnwV+OH0nMqFRuI6f5bwDV8CoAsWdkflPoUhCs6B8S31aqrPSnAU1MsIqbz6qZLaEpjvcPPdsNLvkGAAA=)

```kql
let KQL_Lexicon = dynamic([
    "project",    
    "summarize",  
    "join",       
    "Kusto",      
    "let",        
    "where",      
    "print",      
    "hacker"      
]);
let Assembly_Plan = dynamic([
    { "w": 2, "i": 0, "f": "upper" },  
    { "w": 1, "i": 1 },                
    { "w": 1, "i": 0 },                
    { "w": 3, "i": 3 },                
    { "w": -1 },
    { "w": 1, "i": 4 },                
    { "w": 2, "i": 3 },                
    { "w": 0, "i": 2 },                
    { "w": 4, "i": 2 },                
    { "w": 5, "i": 1 },                
    { "w": 5, "i": 2 },                
    { "w": 6, "i": 1 },                
    { "w": -1 },
    { "w": 3, "i": 0 },                
    { "w": 3, "i": 1 },                
    { "w": 3, "i": 2 },                
    { "w": 3, "i": 3 },                
    { "w": 3, "i": 4 },                
    { "w": -1 },
    { "w": 7, "i": 0 },                
    { "w": 7, "i": 1 },                
    { "w": 7, "i": 2 },                
    { "w": 7, "i": 3 },                
    { "w": 7, "i": 4 },                
    { "w": 7, "i": 5 }                 
]);
range Step from 0 to array_length(Assembly_Plan)-1 step 1
| extend Inst = Assembly_Plan[Step]
| extend WordIdx = tolong(Inst.w)
| extend IndexOrMarker = iif(isnull(Inst.i), -1, tolong(Inst.i))
| extend Transform = tostring(Inst.f)
| extend RawChar = case(
      WordIdx >= 0, substring(tostring(KQL_Lexicon[WordIdx]), IndexOrMarker, 1),
      WordIdx < 0, " ",
      ""  
    )
| extend Char = case(
      Transform == "upper", toupper(RawChar),
      Transform == "lower", tolower(RawChar),
      RawChar  
    )
| order by Step asc
| summarize Chars = make_list(Char) by Dummy = 1  
| project Creative_Output = strcat_array(Chars, "")
```