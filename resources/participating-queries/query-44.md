[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAE1S2U7DMBB8z1dYeUkq1SVAuMVDuQvhDDdCkWlNFUibKNkARXw8a++a0qpxxzM7s3a20CCG5UiLbfGiGr0aZyNtcAZlA3U+HYd+kkeQpP0W13GSx+1gF9cZ4rQPSY6/FLHlDRejJsJ1HfdiQNwyN7b6lGtJi3yEfOy0ttbvbHkFtkWNYGMjBfh9KXSI26DrTUGtia5t3cGO9+QJ/AT9oCv8nvS7Fu0YJHu9nsHBLiFJaI85Kw32bR3+J5sDC5300EolS4+IY9MBIQ48pngp/5xOOJRqE+K59pR8ufaMlIzOiZsbXbA1lV5yS7Y4uGJbCkm5QUtdW+Gfyw0fjJS3rCSXO04g7p7vh7gHPsbc6ZE7oJhFd3AjCJY4hdCyS7Eodtc3t1pxW8YrWHUvzaI1F2PROt8KoQ1Gcv7iIrdl3P3MPBZ873nLq3BMaNy9H6G/QE9HbvibqsghNADVwu+goKrLNz0EqT7VTNjSLMLtyYfUX5VypVAKmFW6fA3dFP6Ioizf28oNcDl1kU07mag6/9Ziot51VuQN8Ej/yxO1btoCTE9QDxVkqq7VLDTijMTU4S+k+eRuugMAAA==)

```kql
let code = base64_decode_tostring("Li0tLSAuLi0gLi4uIC0gLyAuLSAtLiAtLS0gLSAuLi4uIC4gLi0uIC8gLS4tIC4uLSAuLi4gLSAtLS0gLyAuLi4uIC4tIC0uLS4gLS4tIC4gLi0u");
let decode = datatable(letter: string , code: string)
[
    'A', ".-",    'B', "-...",  'C', "-.-.",  'D', "-..",   'E', ".", 
    'F', "..-.",  'G', "--.",   'H', "....",  'I', "..",    'J', ".---", 
    'K', "-.-",   'L', ".-..",  'M', "--",    'N', "-.",    'O', "---", 
    'P', ".--.",  'Q', "--.-",  'R', ".-.",   'S', "...",  'T', "-", 
    'U', "..-",   'V', "...-",  'W', ".--",   'X', "-..-",  'Y', "-.--", 
    'Z', "--..",  '1', ".----", '2', "..---", '3', "...--", '4', "....-", 
    '5', ".....", '6', "-....", '7', "--...", '8', "---..", '9', "----.", 
    '0', "-----", "_", "/"
];
print code
| extend code = split(code, " ")
| project-away print_0
| mv-expand code to typeof(string)
| lookup decode on code
| summarize make_list(letter)
| project result = strcat_array(list_letter, " ")
```