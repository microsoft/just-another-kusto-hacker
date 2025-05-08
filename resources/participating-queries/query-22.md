[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAKWS0UrDMBSG7/cUIVcNtKbdhRcDb32JMUrWZutxSzKSU5jDi6mTKdV7EcFX9BFM18DoGChIIc2X8P/nP5xwTirElRtxPges6ulFYRRXUFjjzAz5Te0wEdpgJW2y8GCSShQLaTlaKbkSoAelQP9NlzKCbOTQgp6TmMAw7Nl4QL+/3j9o3P72ND7gc4dNwMc+Nn3cdrgNeN/hUx/fAu47fD1vFWK8BNz1b4PVw/m6n/9o4STVifNJqvMN7vpWza8tTAZ3RK5R6pJARq5IraEwpczbZWVAo8tn1qi8m5OfHhunE5KQdJ1dX6ZpO8M/qIZ91bGm8GJhrbj1Ul0IjFb+5eSHk4gSymLiX45EUDJfgsO83W2Mli5izLu4WilhYSOJla5eonfzJb1PsFBi0QkjV09DGDGGbNLmjknGfAFK2Q9bOkHY4gIAAA==)

```kql
// https://github.com/microsoft/just-another-kusto-hacker/tree/main
datatable(i1:string , i2:string)[
"😚","😇",
"😈","😋",
"😃","😋",
"😋","😋",
"😀","😀",
"😁","😅",
"😁","😍",
"😇","😌",
"😋","😋",
"😚","😉",
"😄","😋",
"😁","😂",
"😀","😀",
"😜","😇",
"😈","😋",
"😃","😋",
"😋","😋",
"😇","😌",
"😀","😀",
"😚","😉",
"😁","😅",
"😁","😄",
"😇","😋",
"😄","😋",
"😁","😂",
]
| extend i1 = unicode_codepoints_from_string(i1)[0] - 0x1F600, i2 = unicode_codepoints_from_string(i2)[0] - 0x1F600
| extend a = array_concat(pack_array(" "), datetime_list_timezones())
| summarize result = strcat_array(make_list(substring(a[i1], i2, 1)), "")
```