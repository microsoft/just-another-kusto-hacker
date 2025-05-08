[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1UQU8TQRS+8ytee6E120aPHgiChAjFBIQYFUwz7U67A9OZMvPWZYkH4smDFiEexEsvHjQm6klJPPhf+gfsT/DNbFu2UZCk291989433/veN9s1QuFMcWm1XttYK848B36AXIWwEXOu5qA47J+c0PVl2D/+OTh6PTh78fv8GJjhkOoYDGdhGkDE6W8qBi1tACNh52HY752PL1hQGiNuQCsODYHcUhIHqdvXTMsxfCikZG1eX+e6K/lMxnWaJwU+jQLD/vtTev1Br7/y69+mG1vBWQutWAFq2I+5SSERGEGtUqtsVNYKwf/WH5MATaagJSRyM2ZtAxgv7GqhgBH9rIsAFmMhQ2AjNIwYQshbtGQL1RUcHJ1ZuGJDGKVckbFsdAc2uUKhuHRJj5YeeD5UKCVthryJtDHNDS0ozozn12KmkFN7odFgMOck/ujV7H1w4l48/iMK91hzj0ToCOYsQvZIOLQ1sDYjDTop/SiuE68LLRluhUVI2fxUZahp/ALBulRfOx+MitNMVGoEoUH0HahNLfJOwfnpe47/oomVrt9nxoJ3Su/Mz79H/jj9TCCx9e6dJZasww6FagewG1ucjNBv1qV6XoAk4irzeuzvJhM+AKW9ZSMROstq7VWcaGuRpYSVBI0Ys7K9fQltilgYHL29hMXqJSxyzd3VMlyXBO4G9OrlsP/mnROU0EI3cBNL7hESbSRZzgMlOibfSc3CrB03G/Zskhe6ZhKgQdVof+2WM3MZ0Y4wGLfUYs5COlEu05WGdPpBt0C5tGq16ubwNUd1WRiL9S1DA6ZBUJCesHSnuNMobS9UnjzdZpVDd79R3mkUA7gV5CZXvoDZ5E2twgkOahKRm9KleDcrt0eQhOi/beUc2lYkzAjsepzGgucwlmmeGP0NUsq8XM4K3TGaasNaoRV1YNE0GZZy8gRFKAb5Pn0gR9W/57d1wF2jd915HiH/Aati/TTfBQAA)

```kql
print
"DJ_KQL"
| extend Queen= "👑👮🏻‍♂️ are you ready, hey, are you ready for this? 🎸🎸🎸 Another one bites the log 🎸🎸🎸 Another one bites the log"
| extend Village_People
= "👮🏻‍♂️👩🏻‍🚒👷🏿‍♂️👰🏻‍♂️ It's fun to query with K-K-Q-L!,It's fun to query with K-K-Q-L!,You can filter the logs, You can join and extend, Build a query that defends!.It’s  fun to query with K-K-Q-L! It’s fun to query with K-K-Q-L! From Sentinel to XDR, You’ll detect threats near and far!"
| extend Abba ="👨‍🎤👩‍🎤👨‍🎤👩‍🎤 Hacker mia, here we go again my my, how can we resist ya? Hacker mia, does it show again?,my my, you can’t beat my system! 🎶"
| extend Bruno_Mars = "🎙️🎩💫 cause you're amazing, just the logs you parse! when you run your query, no one hides too far! threats stay low,but your kql glows — cause you're amazing, Just the logs you parse!"
| extend ColdPlay ="🌈🐘 we used to rule the world, logs would load when we gave the word, now in Kusto we query right,threats fall down in the dead of night... 🎯"
| extend First_Track = extract(@"\b([A-Z][a-zA-Z]*)\b", 1, Bruno_Mars)
| extend Second_Track = tolower(extract(@"\b([A-Z][a-zA-Z0-9]*)\b",1, Queen))
| extend Third_Track= extract(@"\b([A-Z][a-zA-Z]*)\b", 1, ColdPlay)
| extend Fourth_Track= extract(@"(Hacker)", 1, Abba)
| extend Session = strcat(First_Track," ",Second_Track," ",Third_Track," ",Fourth_Track)
| project Session
```