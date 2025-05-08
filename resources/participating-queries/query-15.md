[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJWQPWvDMBCG9/yKlyx2wJSWUjqEDN7ysXTrEEJRrIt1WJaMTiX43/dsL+1UAlqEnve5e+Upox8/IvXYYX0IyI4g7Ck0hHibr4FblyscvyXD4O5YBkrghTWcKtRooqVUCGwi0yObjgQ3vwRNiEomNM54FbeEA6xJVOGTs4PnoLDOmhyQiGtacicdGHFnsVGVEeLmUA3LLWfj0c2bTZvIknCm6XSQdOy94EpjDFa1/aDBp/V25bXtkGJDImTrlMyorWXwnMvlEyoUejbb1ZA4ZBzr034nOTUmf1ny3JfFBCyJHPWFQ1v+NZ5fLht1qOX8fPmPfX2AfXuAff/FapsfaC3R3uYBAAA=)

```kql
let myPoem = "In the silence of the night, Just a whisper in the air, A coder's dream takes flight, another challenge I dare, With lines of code so bright, Kusto wisdom to share, A digital knight in sight, hacker skills beyond compare.";
let processedArray = split(myPoem, ', ');
print JAKH=strcat_delim(' ', split(tostring(processedArray[1]), ' ')[0], split(tostring(processedArray[3]), ' ')[0], split(tostring(processedArray[5]), ' ')[0], split(tostring(processedArray[7]), ' ')[0]);

```