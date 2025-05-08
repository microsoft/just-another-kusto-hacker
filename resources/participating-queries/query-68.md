[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJVVbW/jNgz+nl9B6MtsQKmbvQBDDxlwuB32ZbgNl9unYQhkm6nVyJIr0U1z2I8fRXttk2aHXYAoikg+fCi+qKrgFySgDqEJnjARxNFh0kABIpoW8AHjEZL1tw7BWY8Qdlm/h4I3TRhjwnLhGOTdBLD9mAG2Y3SwBtURDemmqm4tdWN91YS+6m0TQwo7qu7GREvjA8PF5Z7/hGVnmj3GqnahrnpjffXutw+f3m8+bT/+8ev7zVXfqjeLqoKfsXEmohBPTTR1ndkhEQMN/E1NYKlxLjSGbPBAhjWE5mZW32SVxBxbQ0bExQRwkyhyuBoE5MZ6Khd/LoA/yii90qpW+jutGllbpb/VCuV8p/T3Wt3KSSd7K+d3Sv+o1V7pH/QE4+S4FwAv+yDrICf3vL/WKspRkpVkHfM6ITwI/EHWR4E/yv5ztl389WYxcAhnKeFQB8PZyqkpXiWrXPwNQwx32JyZXf1uqGNh/7DEx8H4FtLgLJ0hZCUNqlIZ58D55NuP0Ry3Dv0tdcUXbJaqLOEnWLEhPhKyg9dqzP3LCCcEL9hzOdNxwLArpuyWuYpy6aNpurmk5wJKYP10fAix/Vc2Y8J0lfOdzHxFb80+XDhgvMCx1IztcxAUeXNJ4yQA2z6ycjT+FotrsV2uNKzKF2FIWT4xmJhnB2M9BVhkUjojZcMc7VtiQT0SZ+apCUC6QGA5xmySGPQu8A3srW/X1nuGPWsZbqfJH6umse9NtJ/xSWk7QWYqfSEtVEJ9FOysj9Eax/pzF9sWeZDUuezsA7ojPA8VLiPLSUiTUxfCniXBQb6gSdQG/w1dwYexr3PaqDP0Uo9ZoM2zBdL9aIR5hN7GGGJ6vrq3nIgOyTbb0whyv6T7SMXpcQnrNdTWF5dkkiN2MoRDkauB0/CcEArz5tzoWq/KUsP/N1hlAyHydY5WX+tImJWvCt3udsV/Xtt6TXFEnUudZy9jjwNP5OK8MK/zXc1kDhfk2fE07M4/WV6elF5v9rh1NlExyaS1uXANzS8Ecrv5BuVVI37O+OfAJf7i2bsw/TZCh8OdJ9kcUPaznTgqUOU/oJC8mEIHAAA=)

```kql
// Get the contest rules, to read every single line of them (of course)
let Contest_Rules_url = "https://github.com/microsoft/just-another-kusto-hacker/blob/main/CONTEST_RULES.md";
// Declare the scrabble letter-per-score allocation table
let ScrabbleScores = datatable(letter:string, score:int)
[
    "a",1,"b",3,"c",3,"d",2,"e",1,"f",4,"g",2,"h",4,"i",1,"j",8,"k",5,
    "l",1,"m",3,"n",1,"o",1,"p",3,"q",10,"r",1,"s",1,"t",1,"u",1,
    "v",4,"w",4,"x",8,"y",4,"z",10
];
print Contest_Rules = parse_url(Contest_Rules_url)
| project Contest_Rules.Path
| mv-expand split(Contest_Rules_Path, "/")
| where array_length(split(Contest_Rules_Path, "-")) > 1
| extend Contest_Rules_Path = split(Contest_Rules_Path, "-")
| mv-expand Contest_Rules_Path to typeof(string)
// Get each of the letters in each word of the Contest Rules Path
| extend word = tolower(Contest_Rules_Path), len = strlen(Contest_Rules_Path)
| mv-expand idx = range(0, len-1, 1) to typeof(int)
| extend letter = substring(word, idx, 1)
// Attribute a Scrabble Score to the words
| join kind=inner ScrabbleScores on letter
| summarize Scrabble_Score = sum(score) by word
| serialize
// Decide (objectively of course) which scores look cool and which don't. Numbers that look cool are either squares or mirrors
| extend Aesthetic_Scrabble_Scores = sqrt(Scrabble_Score) == bin(sqrt(Scrabble_Score), 1) or pow(tolong(substring(tostring(Scrabble_Score),0,1)), tolong(substring(tostring(Scrabble_Score),1,1))) == pow(tolong(substring(tostring(Scrabble_Score),1,1)), tolong(substring(tostring(Scrabble_Score),0,1)))
| extend word = iff(Aesthetic_Scrabble_Scores==true, strcat(toupper(substring(word, 0, 1)), tolower(substring(word, 1))),
                    word)
| summarize make_list(word)
// Generate the sentence, to try to win the contest
| project Contest_String =  array_strcat(list_word, " ")
```