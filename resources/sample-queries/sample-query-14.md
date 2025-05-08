[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA5WS30vDMBDH3%2FdXHEVoorVBH4WB4IPgDxAUfVjnCNu1DWuTkGR2E%2F94E7e1bHbi8nS5u3y%2B903CGLwYLm3FHUJuVA0jLQrwWyHHpHRO2yvGUKaNmAuNM8FTZQoWduxJFJOH0EgH2gjpoEZreYEwhHhh3R1fAZfKlWgaH%2FqMug%2Bp6RxNyVfx4Avqj3Ncai5nYHUlHNkAEoghpr6OS4e%2B2HGdss5LFdtOCl3Xs%2BPG2TfhylfVYOW7t%2Bd81TY%2BD3Gz1v114kZJyyX3HobgRyZ7LHpQ5bEdzaCu%2BBQnBgtcdk6uY5Ke0qAb4uwi7mW1%2Bv%2FkkfSMbpGXu9DuskSekx6J5A%2Fd5IC%2FwLeLuuZGfGLve%2FA5Tiph2zekvSMdNPWejYKvbHzS3hMwBrfowIgZqBxG4%2FX%2FDCJHobOIZI1HRx15Dx1FHRqOYic%2FTAjIdu2yE%2BjY36n6%2B3htAwAA)

```kql
// Translate from [pig latin](https://en.wikipedia.org/wiki/Pig_Latin)
print message = 'ustJay anotherway ustoKay ackerhay'
| mv-expand split(message, ' ')
| extend message = tostring(message) 
| extend StartsWithVowel = message endswith 'way'
| extend StartsWithConsanant = not(StartsWithVowel)
| extend StartsWithVowelMessage = replace_regex(message, @'(.*)way', @'\1')
| extend StartsWithConsanantMessage = replace_regex(message, @'(.*)(.+)ay', @'\2\1')
| extend message = iff(StartsWithConsanant, StartsWithConsanantMessage, StartsWithVowelMessage)
| summarize message = tostring(make_list(message))
| extend message = replace_regex(message, @'^\[(.*)\]$', @'\1') // Get rid of [] from list
| extend message = replace_regex(message, @'\"(\w*)\"', @'\1')  // Get rid of "" from list 
| extend message = replace_regex(message, @',', @' ')           // Get rid of ,  from list
```