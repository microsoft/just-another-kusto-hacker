[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG2SUW+bMBCA3/kVN6SpUHBKEFQpUx6mPEyVtr30sauIkzgJGtiZbbpk6o/f2ZBg2pwUybG/++7OpmYaarETT1pWfAdzWC6X3u3HiOajIB4AXCNIQXqCWMahzgoymUwKC1yYnnqvKIrCZTCiQUGsojCyMYMx9FnYU7dWtz5TjoKgMfIuhEHMb06cmEcYnuMYL3rAMBfFSAYDEUVuP2TUWTRi3hPkchturWvAgHnD/hWiozx8+y9ejV+EaOXPtsGvwb9Pcpax/CFJ8lWWZHm+zfNslqdTem/Ws+whS/Eszba4SvJZvvU7RcurPy1b7KlU6NFCrWlNZWBnlpTvGFSwlaKBBA9BaVkzHgxfYkimuMkOMLUZb8COmvENrPdoU+1KWcpJiKGKYRr29N89k8zAn+Zw84vf9NuqbRoqq38MGvqblYrpYL0PvbBrmUr5nfGdNiVwTU9lbf8GziyIfuw+zc69jvvEqbs2HcFzBZ+HSi+hm1KuxYbZvFp0WWbD7h5ExbUqTc2yl2Lnz8lLCHB3B9+w/a9Pi8dHMPDg3LNjuTppR6qNKEDFmurAT45+7Fxn9+54lXALaQxpiGH0C8FfmdRGBwdaSTM0b5sVk0Opo5DlK62x0qriVJ5K3Aj6meJLI868G2aONphwZVAtzmP2XpM4PN8PphTdmbG6SUr7XoF91bpSOujlYQy+H/4HW25CbuUEAAA=)

```kql
let logoString = ```
*******************+==============-
   **************+=====-:-======---
     *********+=======-...:==------
       *****+=====-:-======-:::----
          +======-...-==---:...:---
             =========-:.:---------
     ------    ====---:...:-----==+
   -------   -   =------------=++++
 ------    -----    -------=+++++++
-----   -------   -    --=+++++++++
     -------   ------    ++++++++++
   -------   -------        +++++++
-------   -------              ++++
-----     -----                  ++
```;
let ourNum = "605e4e59005b40455f5548521a655f58494200524f4940585f";
let uniqueChars = toscalar(
    range i from 0 to strlen(logoString)-1 step 1
    | extend ch = substring(logoString, i, 1)
    | where ch != '\n'
    | summarize make_set(ch)
);
let arrLength = array_length(uniqueChars);
range i from 0 to 24 step 1
| extend ch = tostring(uniqueChars[i % arrLength])
| extend ch_code = tolong(unicode_codepoints_from_string(ch)[0])  // Get ASCII code
| extend hex_byte = tolong(toint(strcat("0x", substring(ourNum, i * 2, 2)))) // Convert hex pair to number
| extend xor_val = binary_xor(ch_code, hex_byte)
| extend decoded = unicode_codepoints_to_string(xor_val)
| summarize Message = strcat_array(make_list(decoded), "")
```