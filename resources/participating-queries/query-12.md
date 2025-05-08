[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAEWQQU4DMQxF9z3F12zaSqMKCrsKCSRWrJFYVBVKO24TJTMOjqfV7DgEJ+QkeKYIVnF+/N+PnUjx0bMSHvBYvXnqUDidQ3dCFt4nakuNoPOC0jpRKCMSZai3FhNDmxOt8MzdXMFnkvEhmqPGS18UiTniyIKLd4rWRTITdcU8r56EDOzSxQ12dKymwC61NQ57ArkSTFHvOgzc4xjEkOq5P3k1AHMqSCESomUxPKUMZ5mK/TCGjWN4Jw3UlVhwJEojdFjhCUIu2eMhWkLDVMYBLixxMpB8f37Zd4arNM1Osqo2s0RTW1NsYSWnoItpfTUqVMvNLEvoFNmLK+NKi8rB6bsTccMiW9hvORG2t+tdfYVt1zd/5d1/eb/eLa/kH6/8oLaoAQAA)

```kql
let quote = @"When solving problems, it's smart to keep things simple. Don't overthink it, Just look for what makes sense. There's always another way, maybe easier than you first thought. Tools like kusto help a lot by making hard tasks feel easy. A real hacker doesn't work harder—they work smarter.";
let words = split(quote, " ");
print phrase = strcat_array(pack_array(words[12], words[20], words[30], words[42]), " ")
```