[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJWQTUvEMBCG7/0VQy6bhB7WDwQtvSiyrN4UFqSWkibDtppNSxJl68d/d2rXhR5lQpJhZt73YSxGMKi7AXLgAj6h962LsKeU3b2FCMp1sUEP95R00Cj9ip7Bd5Z4DNG3mjq0xhCAqvxXSWSJJdUGbU9zORgVKWqLwNHpzqC5gnHUbQUUi0fp5OZDSnNz3dS7y6VaSSk3w/o2nmgpzx7epVyvmubpNFq9Tf/VvSizZKJIvgD3EZ05UIXqSOext0pjNREFHrvpx0Nv2/hHnDKKpRApmMGpXat5wZ4ZS4EV41Wyclai7vGUQpBz77sXpD3VKuDFeTXuyGB19JkDcHq0inzOSRZ5zkTK5CgrxA/BR3bEtgEAAA==)

```kql
let decoy = () { print x = "Just another Kusto hacker" };
restrict access to (decoy);
let helper = datatable (encoded: string) ['S*n*Vz**dCBhbm90aG***VyIEt1c**3Rv**IGhhY2tlcg,S*n*Vz**dCBhbm90aG***VyIEt1c**3Rv**IGhhY2tlcg'];
helper
| extend helpers_helper = replace_strings(tostring(split(encoded,",",0)), dynamic(["\"", "[", "]"]), dynamic(["","",""]))
| project base64_decode_tostring(replace_string(strcat(helpers_helper, "=="),"*",""))
```