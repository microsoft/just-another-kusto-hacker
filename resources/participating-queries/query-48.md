[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1UzW7UMBC+71OMctmEutL+taVFK4H4kQBxQVUvq1VlkmHXXceOHC9sEQcegAqJE7e9lEvprUI9lKfhCfYRsBOX/DS7aqJo7PHM98188oSjhuexPGFvaAJDiKg27zuOfuY8SLViYkLgiPIDJnQAoxaYx1stz7+ult/+eKRD7O7sxiPdbHV+4ZFetvrx+++Xs9Xy+y+P9HPHlUcGedClR3ay1c9rj+y2xo9a3BYiQhlhlFGna6spFWFpq0yOxhVSMpcNzmpe7cyhuDYLjzU1fttEYRyAO6sSVxOaGS/qxDb6v+x3Tjc10RB9VTaN+jVKZZ31Gu4vYmPz64raLMB9JF/b/Gap7DWsXMHWZ+BSzuZJMSJS5GtzlM7jmCr2CeEZmzBtL2xMZ3jMWap9MzCBicGFRhHBSxGxEG2EomKCvhkaqhQ9PeYoJnrq5wDBthmhvk2LP2zjIqEmk4kIFybvFkFL0KcJyve+HceC4VCxxI7Q0AGn3IQ7XJKjOLOVMXycosJqEQ4igOEQ+gXykzRkzOBqaRhvg0adcfBgsA9bNXfXuPfueHvjoKLX0ylVVbkyEhuUKHmCoYa3mM65bUdhwqlp5XF7RGDcJtA2n5b5r8DPkIKSDi+YoNxWa4ROOdXo50gmr9Pt9Qc7u3sP9y3Kq3mqgQqpjRDw2mwkTGk4Q9Uul5HB/QNlQfYnJAUAAA==)

```kql
let EmojiMap = datatable(Emoji:string, Val:int) [
    "🤌🏼",0, "🍻",1, "🤪",2, "😵‍💫",3, "😳",4, "🤬",5, "🥷",6
];
let EncodedEmojis = datatable(Emoji:string) [
    "🍻","😵‍💫","😳","🤪","🤪","🤬","🤪","🤪","😵‍💫","🤪","🤪","😳","🤌🏼","😳","😳",
    "🍻","🥷","🥷","🤪","🍻","🤬","🤪","🍻","🥷","🤪","🤪","😳","🤪","🤌🏼","🥷",
    "🤪","🤌🏼","😵‍💫","🤪","🤪","🤪","🤌🏼","😳","😳","🍻","😵‍💫","🤬","🤪","🤪","🤬",
    "🤪","🤪","😵‍💫","🤪","🤪","😳","🤪","🍻","🥷","🤌🏼","😳","😳","🤪","🤌🏼","🥷",
    "🍻","🥷","🥷","🤪","🍻","🤪","🤪","🤌🏼","😵‍💫","🤪","🤪","🤪"
];
EncodedEmojis
| lookup EmojiMap on Emoji
| summarize Digits = make_list(Val)
| extend Indices = range(0, array_length(Digits)-1, 3)
| mv-expand index = Indices to typeof(int)
| extend Triplet = array_slice(Digits, index, index+3)
| where array_length(Triplet) == 3
| extend Ascii = toint(Triplet[0])*49 + toint(Triplet[1])*7 + toint(Triplet[2])
| summarize Chars = make_list(Ascii)
| project Result = replace(@'[, ]', '', tostring(Chars))
| extend Final = translate(Result, '0123456789', 'Just another Kusto hacker')
| project Final
```