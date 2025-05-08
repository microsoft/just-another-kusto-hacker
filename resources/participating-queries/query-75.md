[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAIVW227jNhB911fM6mVtwJfu6xZBkWbdJG2SpnF62W4WAW2NLW4oUiVpe1X44zvDi+wWiKvAQoY8ZzgznIumUzh3IEDJFXrZIMyXZuNB6AoabBZowazA17RuGgFXqJTURsO9Ne7FtEYX0ykMAscx8tIiLnEI11CLLYJQO9E5QP3FdFiBluuadFdb1H5j0Y2YvZO+hlpWFWrQxqMDbzup1+ANVLjs2pqMaNA5sUY3gdkWbQdsKpOFJuVbVKYl9TvhYGU2uhqB9EESsNHyrw0Cfm3RStRLZLV0AHvIClaSPGWPd7WIHKmdrHB0WGDv0/kTeCD3tFfdCK6ZbkmUWzqbQSujlNmx6Qk+AoX+rWM3bNd6tsqbNRLWvmF2eJ5PPxmX0DC7u3j4eP84+wC3s/n8/HKW1p8SkF7jU0+PpN8eTj37DJ1GASZMn0z4N4ExLdO/40mCJuw+SowMuAnQH4GmhIzkcOg+gJ8iOKpjyjRRWO+YFxk8jfY+RWzQ9pq9CUrY/cmg7nskPP1P/BnI2Kumadg2ukNlzIujinmhZKolZQwn2q2xDuHCVPgGbsKttxZbYZGyy7ICSgVwXnhsKIEc5ReyaH0sgKMkowwMYk7sgpkzHVIIq9sEOoOifOVCTgT/9VDzJoPLb9nYO7Prc5dKBINBBxfBi4Wi9G6EX9aAgl6E9lSoK2OjvCRYsDywAukMKkEBYOogwt87b6leSBGDbo7XhsWngu+nPC9HQJ7SO4jfszgm08NCeRHFcRI/pN2ILmeBS6+o6ocg9uDLAB5n8FXczZqvo5jP/TGaMSZDorKf0smJfRP3M/s26s7suwjO4s9xt9d1n5Qn8i/JsEgvH5LqdNI82ZnExwDOmn5NLqbN3xI2afo9nZN2/0jRSrsfk0e9sj+THZO8ALwwLYvPOUlyh1tYFC8hSRz1Orr1nMvxMimlqe1SsxbWio4HBbVduZXVRqiUVq5rFka52NRDP9Ww2EhVheHkfCYtaUCsrGngm9DJ6US9yXMq6+C0O8ooR5lnhebKqr4ekYMxzwr12tcD1yrpB/8tsxH7PBxSzbwjV7CFd8WeholHno+HE+gAb6KrJxV9IgM+D0dgbBVIJIZIPv5renwx1AF2UimqL+oxjkYlOUrTKBRWjmwquNA9JE3f1jjpJc1mVkgtKdQmT8XcXiwq3ArtMzO1mUN9hsosjgNHzgZjXijyZ1JrYg1CJvSkInbe0yE5Wh4WQyAbj1boDGeoDS66FBbhluzCA7qN8slKDWvBY5P8iakUOCRFCifIqN+Ra636zMufGDzjHTdk4U1wzG2aRlj596HvnjFnKfxzSIwBB/+ZNadmRfdWlkPWNzfx8+CtS4063XWv6br/MPgO3o+H/wBcFOLiZQkAAA==)

```kql
// As a lifetime Scout and member of the Soma Hellinon Proskopon
// (Scouts of Greece) I have always enjoyed night adventures,
// with hidden notes trying to decypher messages. Every time
// an enveloped was found, it was a unique experience to try and
// find out what was inside, what was the message. Recently, I
// received the following message, let's decrypt it together!
//      _______________________________
//     /       ENCRYPTED MESSAGE       \
//    /  -----------------------------  \
//   /  |                             |  \
//  /   |   .--- ..- ... - / .- -.    |   \
//  |   |  --- - .... . .-. / -.- ..- |    |
//  \   |  ... - --- / .... .- -.-. - |   /
//   \  |  . .-.                      |  /
//    \ |_____________________________| /
//     \_______________________________/
//
// Hmmm... it looks like this is a Morse Code! Let's prepare our
// let statements, we start with the message in the envelope
let EncryptedMessage = 
".--- ..- ... - / .- -. --- - .... . .-. / -.- ..- ... - --- / .... .- -.-. -.- . .-.";
// Now let's define the Morse Code table, match each letter for each code
let MorseCode = datatable(letter:string, morseLetter:string)
[
    "A", ".-",     "B", "-...",   "C", "-.-.",   "D", "-..",    "E", ".", 
    "F", "..-.",   "G", "--.",    "H", "....",   "I", "..",     "J", ".---",
    "K", "-.-",    "L", ".-..",   "M", "--",     "N", "-.",     "O", "---",
    "P", ".--.",   "Q", "--.-",   "R", ".-.",    "S", "...",    "T", "-",
    "U", "..-",    "V", "...-",   "W", ".--",    "X", "-..-",   "Y", "-.--",
    "Z", "--..",
    " ", "/"
];
// Now, let's break the secret message string into an array of individual Morse symbols
// and then build a list of indices from 0 to the number of symbols
let morseLetters = range idx from 0 to array_length(split(EncryptedMessage, " ")) - 1 step 1
| extend morseLetter = tostring(split(EncryptedMessage, " ")[idx]), order = idx;
// The following join will make sure that each message letter with its position 
// is matched with the relevant letter in the MorseCode table
morseLetters
| join kind=inner (
    MorseCode
    | extend morseLetter = tostring(morseLetter)
) on morseLetter
| sort by order asc
// Result in then gathered into a sorted order list, into a signle string 
// without separators
| summarize message = strcat_array(make_list(letter), "")
// So, what's the encrypted message I received? :-)
```