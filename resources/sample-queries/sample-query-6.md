[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA7VTy27bMBC85ysWvEgC6EKK5bQF6qIo4Bz6SgLbusSBQNMbSZYsCiTTSEY%2Fvks5Rp0EhttDD%2BJjObM7s6QaXdQWmNUdO%2FsF2FqsV9DCGKwWtamERZ%2BtRZlDYcAqBVKLbcc4sPloep2Un5Po5ibJf4xm31xQrWVXFsIAQK6s3rLgedKlMHgRpyuUaoWpVcZS%2BcxvD2Dd89pZTiADQiNUaAwYKXRffzzJrvIrSKYzsLMwhHCeTC%2FdgcgrKXLboRFaqixjL5If0QDdAW4bEZDWWkibiqrymf8mYNw8LPeKecjjIOCwPT%2BJjJ%2BQw5PIdw5JKtaqqKEs6tUYirpGDf4ZdRSaY3d1zBJLJnaeTPLLWZhM59l4zP6fx%2BFfenzLz3tkfBL5nkfUjQBUvXOehkDqG63WKO1APIpuH%2BfQcuj4fhvRPiLo5ucA20b0Xp0Lp4%2B%2BqN%2B4YeiG%2BE9LLG4a9%2FxUpR5R%2B6RECusT%2BSg3OGhohTWRiUQL36UK4FXq4v7ep%2BMPFxw0NpWQmGrMsO3xHLzS495XL%2BA9%2FZ%2FZa2J%2Fec3eCduTR6B0H%2FpIaWgexP3k8Eqv6LEtu%2F5YGOn0m4fNRuhii%2FCd%2Fj%2BRIaV6UXz%2F3jaixLQqjN25p1v%2B5N0ubhdscXfnkTzvQNOxZE9xR%2BWOA17wG8lgZHCjBAAA)

```
print "try"
| extend x = translate("jakh is too crazy", "U5SPVkBV1QQVhN5TL", "ojcykias   hotrz")
| extend x = base64_decode_tostring(x)
| extend y = translate("ghosts are less scary", "=EgOhO VST tT00 0UVSF", "ahlcahtyesarcogg")
| extend y = base64_decode_tostring( y)
| extend z1 = extract_all("(.)",substring(x,0,4)), z2 = extract_all("(.)",substring(x,4,4)), z3 = extract_all("(.)",substring(x,8,4))
| join kind= inner (
    print "try"
| extend x = base64_decode_tostring( "VEtUVEhFT0VSUg==")
| extend z1 = extract_all("(.)",substring(x,0,4)), z2 = extract_all("(.)",substring(x,4,3)), z3 = extract_all("(.)",substring(x,7,2)), z4 = extract_all("(.)",substring(x,9,1))
) on print_0 
| project-away print_0, x, y, print_01, x1
| mv-expand z1, z2, z3, z11, z21, z31, z4
| extend temp = tolower(strcat(z1,z2, z3, z11, z21, z31, z4))
| extend len = strlen(temp) 
| extend temp = iff(len<6, replace_regex(temp, 'k','K'),temp)
| extend temp = iff(len<6, replace_regex(temp, 'j','J'),temp)
| extend len = iff(len<5 or len >6, len-4, len)
| order by len asc 
| summarize Message = replace_regex(tostring(make_list(temp)), @'[\[\"\]]', '')
| extend Message = replace_regex(Message, @',', ' ')
```