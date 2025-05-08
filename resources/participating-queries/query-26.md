[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAF2SPU7DMBTH95zi6U2tlKFxPyhFvQBXQKhyEwtMEkdy3KGIgYEBCVo6IUBIMFAmRk7ECTgCL05i0ybLL3p++X/ImTAgVFwkIoEpJNzQO89ER06kMiGUy3xeZJPSaKnOusFJAPT0QsDft6drDCGy+HlDyCxuVoR9i/ffhAPCn69XDO3m0A5WaxqMLG5pAgf15jPh2G8eWnx4b1ajWnX7UqnWsh+PFbNWAaJad31X8cA5q9eH3l408irRP/Fo7H+1p8563jmr1Te3FTMvyfreIRu0DoPToyCjkhNRlax3St5pNwQ6ZoTeK7tpGo/RBcIFujBYoguDBtsACI3xxjRydH2jQpcZC3RB8RxdABR+v6oZNbqgmKIrAGMbsLlBwRVcFFJBKlUylUpR3DZ2oZq7RGfKQhuYL0ECL+Pqe5HnXMtLAVqUi8xQR9RBzM2Ma82XnZynYpbJ0nTqhrokj93gD2I5M8q7AgAA)

```kql
let encoded = datatable(i:int, symbol:string)
[
    0, "😀", 1, "🦄", 2, "🐍", 3, "🌴", 4, "⬜",
    5, "🍎", 6, "🥜", 7, "🐙", 8, "🌴", 9, "🏠",
    10, "🥚", 11, "🤖", 12, "⬜", 13, "🎋", 14, "🦄",
    15, "🐍", 16, "🌴", 17, "🐙", 18, "⬜", 19, "🏠",
    20, "🍎", 21, "🐈", 22, "🎋", 23, "🥚", 24, "🤖"
];
let decoder = datatable(symbol:string, letter:string)
[
    "😀","J", "🦄","u", "🐍","s", "🌴","t", "⬜"," ",
    "🍎","a", "🥜","n", "🐙","o", "🏠","h", "🥚","e",
    "🤖","r", "🎋","k", "🐈","c"
];
encoded
| join kind=inner decoder on symbol
| sort by i asc
| summarize result = strcat_array(make_list(letter), "")

```