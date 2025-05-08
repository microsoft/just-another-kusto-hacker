[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1RXU/CMBR951c0fRqBhI0NFh94mLKYuBABRYIxWbrubiuwbrRFPuKPtzWCUR/gPrQ5t/ecc9MjCM8BMZSJqkQOUhVybF1IKqiR0/hAsFfAU5QrNNCvUgnGc6sgsohlQbq9vsVhF+dbllrNZvNn3oxTIsHSRFpxRRiXCDuu6+M2wvCwu2F2GOF2A/2rXwxqp65h5GEwCvzO07zTZ2IfTG9H93dC0NZ7cVkj8VItgfBqNjzK+rDoRSvvcJmWEQrGmqdDaS+j4WRR7yiZXMFMADLD3Ljz1nL78lzwcbjIlo9T1+tUUWt8hbdtm53xfv6azDbbIAsngwFuY2y+eFeA0JlJXikoa3WwlOnKbVkSwY6ABNRrvXv8HdYfeFyzJE6BVmUtQMrYJB8nOqq+dxo550yEIAfTpUSdQCVUTCS1SrLSmqC0e9MsZs63vU+xuUiKv2DXP8NPmCOusWoCAAA=)

```kql
range i from 1 to 10000 step 1
| extend gt = tostring(hash_sha256(new_guid()))
| extend t = case(gt contains "1337", "eJw9i0EK",
                  gt contains "c0d3", "gEAMA7/SW/6irxARBMGCrrc+vh",
                  gt contains "b4d",  "kUDzspyY5Kk4y",
                  gt contains "face", "ndDs0jKDQYpwcaQy",
                  gt contains "beef", "q3W+juVThnPEYfjOR34/oK+P",
                  gt contains "f00d", "xWZbUquAfEQ==","")
| where isnotempty(t)
| summarize replace_string(replace_string(zlib_decompress_from_base64_string(tostring(array_strcat(array_sort_asc(make_set(t)),""))),"\x7c","\xad"),"\x27","\xad")
```