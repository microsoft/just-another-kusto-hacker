[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHWRz0rDQBDG73mKIZckmCdQCp4rnjzWUNZ0aNMku2GzARFfQMmhhx6KiCIIClUfwWfyEdxmZ3V6aHL4mGF2/vy+oEIDWKtlASOYCWP/qwrjIXMMrdGFnCcwCcB+0c/z5i5Kd7r6crr+oPiT9Nvp5oHiN9J3p72veyF9It1SP3rf31MfmrOiOWt63/t+vt73o7mbR8q/ktKcfhsF2UmwO7rGthVztGeH4641IKQyC9RwZgMFC5GXqENXOtCY1qI5zCiFxoq5GIKD4MacXscRtpyj4TCBExUcq+RsFQfsGwxUFhw1ct6aQwdO/ozj77gHLTfCcDf8Bnvd9jbgJziHcm5Tyb3CP8OGRXeuDcCDW1iqQkJZyNmokNI69m+PkuCL2q6uhS5uEM6d0SONTSVynGqc43W8HxnlHItrUeK0KloTMz+TJIXTaDIJ08sss/uEoUscZe7UxM5rtFpibvy0X+YOXXBYAwAA)

```kql

let emoji = datatable(emoji: string) [
    '😉', '🐮', '🔬', '🐭', '🐾', '😚', '🐧', '🐨', '🌭', '🐡', '🐞', '🐫', '🔾', '🌊', '😮', '🐬', '🔭', '🌨', '🌾', '🌡', '🐚', '😜', '🌤', '🌞', '🌫'
];
let message = "Just another Kusto hacker";
let emoji_map = datatable(emoji: string, printString: string) [
    '😉', 'J', '🐮', 'u', '🔬', 's', '🐭', 't', '🐾', ' ', '😚', 'a', '🐧', 'n', '🐨', 'o', '🌭', 't', '🐡', 'h', '🐞', 'e', '🐫', 'r', '🔾', ' ', '🌊', 'K', '😮', 'u', '🐬', 's', '🔭', 't', '🌨', 'o', '🌾', ' ', '🌡', 'h', '🐚', 'a', '😜', 'c', '🌤', 'k', '🌞', 'e', '🌫', 'r'
];
emoji
| join kind=inner emoji_map on emoji
| summarize Message=replace_regex(replace_regex(tostring(make_list(printString)), @'[[",\]]', ""), @'[+]', ' ')
| project Message
```