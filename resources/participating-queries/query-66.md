[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJ1VXW/aMBR951dEeSISe9iH9tCpDyt0VaWuIILKtqpCl+QSPBw7unZSQPvxu3ZSWtJ0W0fQlXx8fb98jizRBsWawOBXKILTIAXL31Jiv0ZPjCWhskGQrIFMs4p6t72Af+FQiqLYzdfCFEgmHARh7MznfUk4W5cqRXJr5Xc4AE60UDYuIFujtcLBN87MEHIzA2WpzN16Hw7Cib5H8v4TUCJxcOrM+TZBGWtKkHY+GZu6mrlQqb43c5FlEt3WpfdPMxyvLqSu3S+cGa9WIuFipEXKUBjrwC9+R+GIRIXjCmkl9b3DSmdGuELXz0hU4NZLZ4aaLCgYamUKQZD4DO/DQV3PFDMOTbspZL6cqe9XmBJkbMtU6Bs+jluHamcmYJP1rESTwm4CZH20Hz751dWIIPeJvz2EH5dWar0ZL6WohPYzPvfDBLNZAvE4Mx/WN3fG13YmDzfytm6pGhdmhFaXHvQzjktaQYKxQtz7qquHfHwcTUKI6gykBH8Z6/r2JObIjc40KUh90u/OXGuLBaTXgiqekkPeeRiUjpF4wtc8OOS/Q6XvtlQ4RVMSYWKbprKHAi6VRSlF7E5c5oXUpvE4DXt3n3ryQOUhU29jjticOOgkSHcKcpHUBG4W/dsOHrcp/AJ728TtIG2bry920b1xFw2OSn1G8ha/O6ndxeo2oTu53KZwN3s7ifuUs8+V+X+9dlC+zfYW0dsc/6cujzXw2hvo0kkX1iWb54pp9/cH8bR77RLTq9nnlPVUVb1fQV69wW0BKm3kxkLz8uIt3Fp8iltdvxjNaxKxy09WR7DhGZ4KpZCC/uPz8/fzUaBVs8uhTJnnQGKPwZKBjx/Yl8+wTcAugAh2/Rw2uJB8u33/gEXcaRgFy91jZF969Fh7iolOMeVAddBFDSwOBw65oqMSiCct7cv5m7h1Bb8Bh/HJW3cHAAA=)

```kql
let phraseMap = datatable(phrase:string, chars:string)
[
    "ClippyWhispers", "S", "AzureThunder", "n", "SharePointSpaghetti", "V", "TeamsTantrum", "z","PowerPointPanic", "d", "ExcelSorcery", "A", 
    "WindowsWiggle", "I", "EdgeOfGlory", "G", "OfficePoltergeist", "F", "OneDriveOverflow", "u", "DefenderDiva", "b", "CortanaConspiracy", "3",
    "RegistryRage", "R", "VisualStudioVortex", "o", "PatchTuesdayParty", "Z", "DLLDrama", "X",
    "OutlookOblivion", "E", "TaskbarTango", "t", "BingBlunder", "1", "DevOpsDetour", "c", "SurfaceSneeze", "v",
    "BluescreenBallad", "h", "TelemetryTornado", "Y", "NotepadNirvana", "2", "NanoServerNonsense", "l", "ZuneResurrection", "g",
    "IntelliSenseImplosion", "="
];
let phraseChunks = datatable(chunk: dynamic)
[
  dynamic(["ClippyWhispers", "AzureThunder", "SharePointSpaghetti", "TeamsTantrum", "PowerPointPanic", "ExcelSorcery", "IntelliSenseImplosion", "IntelliSenseImplosion"]),
  dynamic(["WindowsWiggle", "EdgeOfGlory", "OfficePoltergeist", "OneDriveOverflow", "DefenderDiva", "CortanaConspiracy", "RegistryRage", "VisualStudioVortex", "PatchTuesdayParty", "DLLDrama", "WindowsWiggle", "IntelliSenseImplosion"]),
  dynamic(["WindowsWiggle", "OutlookOblivion", "TaskbarTango", "BingBlunder", "DevOpsDetour", "CortanaConspiracy", "RegistryRage", "SurfaceSneeze"]),
  dynamic(["WindowsWiggle", "EdgeOfGlory", "BluescreenBallad", "BluescreenBallad", "TelemetryTornado", "NotepadNirvana", "TaskbarTango", "NanoServerNonsense", "l", "DevOpsDetour", "ZuneResurrection", "IntelliSenseImplosion", "IntelliSenseImplosion"])
];
phraseChunks
| mv-expand phrase = chunk
| extend phrase = tostring(phrase)
| join kind=inner (phraseMap | extend phrase = tostring(phrase)) on phrase
| summarize base64str = strcat_array(make_list(chars), "") by tostring(chunk)
| extend decoded = base64_decode_tostring(base64str)
| summarize result = strcat_array(make_list(decoded), "")
```