[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHWUW2vCQBCF3/0VIU8RLLgbtZXiQy/2IsVKBaGIhHV3UNskK5vUIvTHd2dp04d6Xj6WnJ05M5NMcqqjyUexzsmMS20NmdnWqYqiUWSOpSp2OlnGRdyJ4hEjZ6SMe8YLQzBeGQtGl2EYY4ZusGmyhHuPjDljzVAM2dwL6hNjynhgDJtTgGNMGHeMA8MyinjVvmzlvrOpLW/slhyV9bVvatDzbVW106pOTjW9FHLVaZ1Uuki4QEIKQ86RIAVMBgtLe0gR0AeGSBgyhC4prAyGDKA/rgxmkzBbCscJpynhS5PwRfehP54AHGcKswnYjcCfAG4HViBhBXDQAs5Gwknjbvq/23tL4bnf3Cul3z+VM1WzxetwyEy4ktXWb/Wu3CT/Fv4n1czZPbn8+OyMF83c61Rq+vsdODqQqyiBnm2fae89YK7WV7R39o10febtVUHRYmdz5S1CWNb9BhmyqSlrBQAA)

```kql
let JumbledEncodedPhrase = dynamic(["m", "=", "l", "3", "G", "R", "1", "Y", "V", "0", "d", "E", "c", "c", "g", "=", "V", "I", "S", "b", "a", "2", "g", "I", "L", "N", "H", "9", "H", "H", "r", "J", "F", "v", "o", "m"]);
let NonCoherentBase64 = strcat(JumbledEncodedPhrase[12],
JumbledEncodedPhrase[0],
JumbledEncodedPhrase[8],
JumbledEncodedPhrase[30],
JumbledEncodedPhrase[7],
JumbledEncodedPhrase[21],
JumbledEncodedPhrase[32],
JumbledEncodedPhrase[34],
JumbledEncodedPhrase[17],
JumbledEncodedPhrase[4],
JumbledEncodedPhrase[27],
JumbledEncodedPhrase[9],
JumbledEncodedPhrase[13],
JumbledEncodedPhrase[3],
JumbledEncodedPhrase[16],
JumbledEncodedPhrase[24],
JumbledEncodedPhrase[23],
JumbledEncodedPhrase[26],
JumbledEncodedPhrase[31],
JumbledEncodedPhrase[2],
JumbledEncodedPhrase[20],
JumbledEncodedPhrase[28],
JumbledEncodedPhrase[5],
JumbledEncodedPhrase[33],
JumbledEncodedPhrase[19],
JumbledEncodedPhrase[35],
JumbledEncodedPhrase[11],
JumbledEncodedPhrase[14],
JumbledEncodedPhrase[10],
JumbledEncodedPhrase[29],
JumbledEncodedPhrase[25],
JumbledEncodedPhrase[6],
JumbledEncodedPhrase[18],
JumbledEncodedPhrase[22],
JumbledEncodedPhrase[1],
JumbledEncodedPhrase[15]);
let DecodedBasAackwardsBase64 = base64_decode_tostring(NonCoherentBase64);
let ProperlyOrderedSentence = strcat(reverse(DecodedBasAackwardsBase64));
print ProperlyOrderedSentence
| project-rename Viola = print_0
```