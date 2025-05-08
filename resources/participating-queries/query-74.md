[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHVVa28aRxT9zq+4QlUNEo4BFz/S9gMmhGLHsSWUJlVVRcPuABOGme3MrA1Rf3zPnV2zu5ayfGF2z7mPcx9zdkb3KnHW21U48TTqnx6kcPTN5s7IA+1ElsmUgqX2be4DCWPDRjq6w8HSRiRb6dqtszO6Y7DSEq+N9KRMw+xG4b070LMKG0qsc9Jn1qTKrEnLEKTzrRb+1C38TqkI+C217PyFkN4qE3owWgLe+uBA79GHyC+P3dbfLcIzuL4c9ah9DIFWNjcpElke6EZpTTMR4EOYlB5FrmmstTRtMG7bvdLAVR/H98ohaXiWzoigrBGa7GqlEskZ3opMRFZesQbsdnH67mFBgzd90iI3yQaOY+bzm3t6nDDDV4zzRqCfrUvJSS2FB2tlHRXWmBQqEmf3WZnUPvvoZ/ZpfvTFUDpCrzmPhyJmn6sgKZXLPHjqsKseTfeJ1F3miIpTN389oiVr62kRhEONpMkZbir4JY5/Kp9DnUXIU2VZMmfTPClzSOWTZ44tOcN+f1Bz8eURKadypbjwqfTbYDNq5gwGB/Vlafd0ftGn3DxJ9EJhfi12CJDhmwp+heP4e+4kJdrmKWVaBIB3qLpBNySFUPJIGNSEOr8YlaxCsgbFVRROYrE9ZEAk/+bKlfH8dPVmdFMvA6BDhuZuJWA+dnUgjXxrSjHhriL8wgQRDoI+ilRqLciIHRxMpg/1ngOy0Qy1nhOeVk5KyrO1g4l634F1geMHZbYynZtX4Q8vbpraD1jMmQp/5MtX0Msy06qyg+uj8GOXkNxjSFKsgAO6KC1UbUoz7DcmIENV1+iDRLilNWTkGpP3pMKhWd9hvYEGg0pHD8ozfZrXWxpw1n+csCWPOUaXoVmX1npMQtE+aEGRbJiVVCwezonNlLaBxnPsQat9JTB2QNEwzNpWLC4d0Lw3oHzgUnB2WDhYPVkMM/hm9w25iKM+lgR6TT1hIwrsS4ymXEYLReO1/vm11aqWZOs/yBsktli0Ml5LrE1elnRarMD4euoEXidYKJ145ieCfntZD1Ph9IFmzj7DP+BlVDUg5qlf0/udhWICA/EjdOzeKZc+qv0DVCzKJM7ZzyxvE9b+iORoJo10cffGz/FrF4lDxm8yCdFY7V54uRB6rEaPKcD6fLcTTn2XhU730nsRtcKtkYjwVTgnDp2d2MqvGjdVpzDR7dHJSbeIh70skM2R04EA8V4Cqn2K6uzEvjh3j6pPsDMCX2QJ/+ngTfntGO0LogB0q3pOLHpnHyp37fviJl45u8PovDLB81S7O8tua/eOUTCgGjEIiv2Pzy9p4XO3XVe1lOh/dj41th4IAAA=)

```kql
// Microsoft's 50-year journey mapped to "Just another Kusto hacker"
// Key milestones in Microsoft's history with corresponding letters

let milestones = datatable(Year:int, Milestone:string, Letter:string)
[
    1975, "Microsoft founded by Bill Gates and Paul Allen", "J",
    1980, "First international office in Japan", "u",
    1981, "MS-DOS 1.0 launched with IBM PC", "s",
    1983, "Microsoft Word released for MS-DOS", "t",
    1985, "Windows 1.0 GUI launched", " ",
    1990, "Office suite debuts (Word, Excel)", "a",
    1995, "Windows 95 brings Start menu", "n",
    1997, "Visual Studio introduced for devs", "o",
    2001, "Windows XP redefines desktop OS", "t",
    2005, "Xbox 360 unveiled for gaming", "h",
    2008, "Azure cloud platform announced", "e",
    2010, "Office 365 cloud suite announced", "r",
    2011, "Skype acquired for $8.5B", " ",
    2012, "Surface tablet line introduced", "K",
    2014, "Satya Nadella named CEO", "u",
    2015, "Windows 10 launched as free upgrade", "s",
    2016, "LinkedIn acquired for $26B", "t",
    2018, "GitHub acquired for $7.5B", "o",
    2019, "Azure Arc expands hybrid cloud", " ",
    2020, "Microsoft pledges carbon negativity", "h",
    2021, "Windows 11 introduces new UI", "a",
    2022, "Activision deal boosts gaming reach", "c",
    2023, "Copilot AI tools launched in Office", "k",
    2024, "AI integrated across all products", "e",
    2025, "50th anniversary celebrated", "r"
];

milestones
| extend 
    Age = Year - 1975,
    Era = case(
        Year < 1990, "Early Growth Era",
        Year < 2000, "Windows Dominance Era",
        Year < 2014, "Expansion Era",
        Year < 2022, "Cloud & AI Era",
        "Next Generation Era"
    )
| project Year, Milestone, Letter, Age, Era
| summarize 
    Message = strcat_array(make_list(Letter), ''),
    YearSpan = strcat(min(Year), "-", max(Year)),
    EraCount = dcount(Era),
    MilestoneCount = count()
| extend Context = strcat("Mapped from ", MilestoneCount, " milestones across ", EraCount, " Microsoft eras (", YearSpan, ")")
| project Message
```