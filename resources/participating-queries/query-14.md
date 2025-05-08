[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG1QS0rEQBTc5xSPAaGDDsTPRsSzND3JU9pJf+h0dCKuBBERVyKIC7OZzAUEQfRQOYKvJzMJaAKV7vepSqVy9FB44WU6xwpOYf/g+DBJTiLrpPaAOnWV9ZjRBCZt3Xy09aomvBNeqb6j857wsuk3hLduFnaaJ8IX3ZeERwLVq4e2Xn5T/4fwuZnfEoLW8yS6AVx41BmUWqYmQx5e1pCdglz8b/IzZxQvPBk+Z73hmHTU5VRYm1djSkYDi4CeAp0UubxGgIVxXQjOXHFdqhk6Fq+Xek9rddqYSS1cxYnBOtbeEOIOHCV/aBkOOY6YmQIb6LvdR7YKRamUcMGfEnPkuSw86+XiKPyndeYCUz+WjTfbZAKRD8Rf9htoKfgBAAA=)

```kql
let statickey = 129300;
print encrypted =  "🥳🦟🦞🦘🥅🦇🦕🦟🦥🦚🦘🦞🥍🥹🦤🦋🦍🦉🤻🥼🥶🥹🦂🦅🦓"
| extend unicode_codepoints = unicode_codepoints_from_string(encrypted)
| mv-apply unicode_codepoints on (
    serialize  xorkey = row_number()
    | extend crypt = binary_xor(xorkey,statickey % 40)
    | extend decrypted = unicode_codepoints - (statickey + crypt)
    | summarize make_list(decrypted)
)
| project unicode_codepoints_to_string(list_decrypted)
```