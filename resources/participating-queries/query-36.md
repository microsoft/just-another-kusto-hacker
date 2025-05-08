[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG1SS26dQBDcc4pWr0DqSAzvi623yi5RVllkEUXRmBnnjU0GBGPpWcpRcoCcKydJTWOsZykg0U1PV3UVTe8TdWc7zXQiZxPuu96XwV1uQkxC3eB8zqriK9Vy2AoZMeYg1CDshDYIe6GtbBqhnbQ42aNUCx0QjNBxaWjF1BlcIxopiEzmyZVGoWYjB9ChouygVnqzX+Dmhc0cl+6FDjRNrTMbI22LAFV1ft3oGGoy3Za+3RY9bNq5C+GTHd84XQ3C6vlmTlOIP7JXTGFiuNgKf0DMqvhJk53wrMleOCHBfLZaqIWjJkZ4YHUJlXzONchhr4eoTJkZPB/1BPjHzNMKd7yK/WkvX4JLZ4g91reFrqj4RQ9DiPQYojuFGP1E5WqqoiHqttDkL8lHR/NoO/85TaCAsc6m73aa7HM5+dHbVKo/LLoSYq6uYOm59+49BgIY7u/LDiJOpO36WMhK/vv7D+fPhnJOqyuO0Trn3evgcpUiV+xX7X2Ib4SWCx7dT3fLTqD2PxfG4097/VTvMrz38QVeqaJxGh58l9YZ/wAyxIYq8AIAAA==)

```kql
let chars = datatable(idx:int, code:int)
[ 0,74, 1,117, 2,115, 3,116, 4,32, 5,97, 6,110, 7,111, 8,116, 9,104, 10,101,
  11,114, 12,32, 13,75, 14,117, 15,115, 16,116, 17,111, 18,32, 19,104,
  20,97, 21,99, 22,107, 23,101, 24,114 ];
let asciiMap = datatable(code:int, ch:string)
[ 32," ", 74,"J", 117,"u", 115,"s", 116,"t", 97,"a", 110,"n", 111,"o",
  104,"h", 101,"e", 114,"r", 75,"K", 107,"k", 99,"c" ];
let maxWidth = 80;
chars
| join kind=inner (asciiMap) on code
| extend spaceStr = strcat_array(repeat(" ", idx), "")
| extend styledChar = iff(ch == " ", " ", strcat("✨", ch, "✨"))
| extend padded = strcat(spaceStr, styledChar)
| extend lineStr = strcat(padded, substring("                    ", 0, maxWidth - strlen(padded)))
| project lineStr
```