[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH2PQUvDQBSE7/0VQ04JptRYCkIRFMGD1T+gqLxsX5rVbbK8falV8uPdhmAvpcedNzPfrGNFMELb0vEaN0hWO+36svWdrUL/tNPW97ZcuyokS8xmuCcOJDDW1ywxkTKZGo5VWRBqW2kUyx9cFNkkqqjsfuhVoSY4Uk7/afk5WDw+dkFBTauRhFV8tKjJfLEk2XIS6zYMi0raLQrEW4Gg7FFMevBeuVlD6DuShwVH0TimZpgk7B0Z/hDe8D6N5hy3yes7TX/vpi94O0xIsmPQk2gRY6Erg4ptNulYleMyxyLLB8fVaccix/XomJ92FPMDy0v7yUbxYBtyzxwCxV9Gv4ohTYcJI2csy/4Ais+BhcEBAAA=)

```kql
let scrambled = "Kvtu|bopuifs|Lvtop|ibdlfs"; // Caesar ciphered (each letter shifted by +1)
let fixed = translate(scrambled, "Kvtu|bopuifs|Lvtop|ibdlfs", "Just another Kusto hacker");
range i from 1 to 1 step 1
| extend raw = fixed
| extend cleaned = replace_regex(raw, @"[^a-zA-Z ]", "")
| extend part1 = substring(cleaned, 0, 5), part2 = substring(cleaned, 5, 8), part3 = substring(cleaned, 13)
| project FinalMessage = strcat(part1, part2, part3)
```