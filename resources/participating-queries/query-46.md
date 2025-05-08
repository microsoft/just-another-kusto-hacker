[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHWTb2/TMBDG3+dTnPKmjpQxsQ00DVUaElAJxBuKhtA0omtybb05cWRf/018eM5OmtIVkle2n/vd+bmzIYYplY74K3mPC4IxVMjyzwwpakpbUXXj2elmkUNrvWZtmxvdcJbcJyBfOm3unqv343Gaw+schu/8HNLPK89pp/r54826mixNuYjKi/ygwsbyklwvnF4KbnIdRJcvcF8EZ3sZTj494sXdTmRXcCxbYvkUcA/vkkTWH+R6u5YBmwrYYePn1tUgGaHurpwcGZD8BtoyiTjpgQIQF2LEDD29vYIWHft4XMWzSlzrjopuo2Dbeba3MDvFftxKNSXDXDvPUC4xrMiBqqi2jYRjsDqL8qgpgkYyUReo0l/qVda53peR5S/haAys7YaM/ye3PxqYhehVqu6RtF09BPgJ+Ru1BkuCEY5go3kJo9sRMNWtdei02UVdbSs919EX1+kLRwvaqh6XSwMFnt6mB2P2Caat0QwyYfZgSmd2WIZifVCofQ7BREq9PqNtG7ocdaeGfw/NN8gUS57JlIDkkHtEgSMZLhdL5r1QSYF9qUNDIzwLCf2qruXKzwQb60KcKEoUD53DnarxiQqjPas9OYuVwmw3vCOBSKT0/K89QF8ewevhYf6HH7IHNkQbZDb9ISh2SApYGe5fcZA4+0gyHN3+H8SGzT8DBAAA)

```kql
let SecretMessage = datatable(encoded:string, position:int)
[
    "SnVzdA==", 1,          // "Just"
    "YW5vdGhlcg==", 2,      // "another"
    "S3VzdG8=", 3,          // "Kusto"
    "aGFja2Vy", 4           // "hacker"
];

// Decrypt and transform the message
SecretMessage
| extend 
    // Decode the base64 parts
    decoded = base64_decode_tostring(encoded)
| extend 
    // Extract first character (demonstration)
    first_char = extract("^(.)", 1, decoded),
    // Extract all vowels (demonstration)
    vowels = extract_all("([aeiou])", decoded),
    // Replace 'a' with '@' temporarily
    modified = replace_regex(decoded, "a", "@")
| extend
    // Split into characters
    chars = split(modified, "")
| mv-expand chars
| extend 
    // Translate '@' back to 'a'
    restored = translate("@", "a", tostring(chars))
| summarize word = strcat_array(make_list(restored), "") by position
| order by position asc
| summarize message = strcat_array(make_list(word), " ")
| parse message with result:string
| project result
```