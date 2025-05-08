[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAIVSS0vDQBC+91eMOSVgCeit0Jt6sAcL4jkMyaQJTXbD7qa24lXP3n2AtoWCiP1J+SlO0mdIwMO3YXfne8xsXPcqFpjAMEKlqQfXuTaAQpqIFAx4IyFCf0yq47qdTMXCwKXwZUDBBRqEPljF4hmK+SvjnfEGxWLN31/GF+NzczZfMb4ZH5v7xVOdU9ZVvNWW+8NY7jhW5xFoakgEMKDZJmplvXyxwHXhJu3BnYgnpDS3citzLpQhDAl9OlADqnIfK+QiLs+8cskkN6e9UMnU04Y7Hdn7UodV0kmXphm2CfGQzCwjGdqJFCOnYbkd1T9uR3Nt9atUmlb3/FJUqznpw/lZI8S+6Ub87jH7wPPL2/bYRu5C18TLODpPU1TxA0H1Y2WRwtKVy300HiqFMzvFMXlJrI1deTinYFnOH6LxrjmKAgAA)

```kql
//Final Pharse: Just another Kusto hacker
//
print EncodedData = "आ ࣛ ࣝ ࣜ र ࣯ ࣢ ࣡ ࣜ ࣨ ࣫ ࣞ र अ ࣛ ࣝ ࣜ ࣡ र ࣨ ࣯ ࣭ ࣥ ࣫ ࣞ"
| extend KeyPharse = "ॐ" // Om: Universal Sound of Peace
| extend decodedKeyPharse = unicode_codepoints_from_string(KeyPharse)
| mv-expand decodedKeyPharse to typeof(long)
| extend decodedData = unicode_codepoints_from_string(EncodedData)
| mv-expand decodedData to typeof(long)
| where decodedData != 32
| extend decodedPharse = decodedKeyPharse - decodedData
| extend chars = unicode_codepoints_to_string(decodedPharse)
| summarize Finalphrase =strcat_array(make_list(chars), "")
```