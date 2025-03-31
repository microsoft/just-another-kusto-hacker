[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA22RQW%2FbMAyF7%2FsVhC%2BxAcdYgWG3ADt32KmHHeIgoGXaFmxLKkV1STD0t492k2UdepEFku%2Fx81Ng6wR%2BUIzY0y57xMsFGjRjCoDmOVmJgJYNYycVYBzBeHbQEBrvAJ2xpPJmStTZOKwSVENqdTba2U4oniv4TtzgBKhdh0kAm%2BinJBRB2KY5DKgu6hiJX1CsdzbqugFDOMOIQ3IYYbaxtUxGoE1zE4WTGSEQd55nBVGvMHjxnVXxQFxl8Ok3zC9bOgV0LTwpKK1jO4hhspIzhQkNHZl6OuW26%2FJrDECujb%2BsDJBVWQkxLdus62%2F9Ej5rVXgidysVsIWHorwFqbesritQtVoUb6fi0EkZ%2FmMRNij535LOwus6fGf%2F6bm9c78bXcyta%2BmkbUbXU65syIzno%2BL1MuQfilbeUpFBPMg5kO9yfbevX5bFMc0zsr3Q7XcW73dhib8mMuNIx0lfa83vyrmD7DVb9%2Fwb3tpU2G7ZtALvlhzvUX4IuhevXG%2BK7UNxKIqFulg%2B3zb7el9ndVkfDpsSNpviDw8tTCbNAgAA)

```
print Message="Jazz backup acquits aircraft. ask corn beacon ancient bluefish acquainted assimilator. Kerbal aquanaut absolutes triumphant conservationist. happy kahunas misdirect dumbstruck performances photofinisher." 
| mv-expand Sentences = split(replace_regex(iff(Message endswith ".", substring(Message, 0, strlen(Message) - 1), Message), "\\. ", "."), ".")
| extend Sentences = strcat(Sentences, " ~")
| mv-expand Words = split(Sentences, " "), index = range(0, array_length(split(Sentences, " ")) - 1, 1) to typeof(int64)
| summarize Message = replace_regex(tostring(make_list(iff(Words == "~", " ", substring(Words, iff(index == 0, 0, strlen(split(Sentences, " ")[toint(index-1)])), 1)))), @'[\[\"\,\]]', '')
```