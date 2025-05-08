[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG2TWU/jMBDH3/sp/NZW6sOm3KA+AMu5HC03i1aVmwzFJUexXWgQ73wM3rjFtUIc0mq/Eh+BmYbUiaijGSX+zd+eGTsuaFYWYINiJeZwjU/NhdyUFzTEqNJS+PUCK3Opux/L0gE5Knyd38kwHNmPs9NztPdsgWVLJfRWoQsu0G4JVH6jLxpwSSoC4R76PgOu0K4JzNro+w24Rnsl0NpAP2DADdpLRzGHftCAW0qAgHDQDxlwh/ZGwKOshg24R3smEFBWIwY8xHtM0x7WD0Oe0P4RceeJJGr/i/ZIZIu2t4pp8p+I39Ekqn+ONZvbRBLlv8Qtbk0QSdT/GncspGqsRAPe4qw9KsdKdOA9bmaRmmkNZ/6MZZp4vhqPV9SFz901aGu8ElpyX7lcQy7S8prtwG59TzT2Xc8PmgdS6dbhUTs8Hp+Y/Dk1PTM7N/9rYXFpuVxZWV1b39jc2sasIm0qPLVQKjy10Je2xhUM9lcdsAMHqjqILmOUEw0JhyAVmAkaGGZzl8v0LI3oxn+bPmEBXW5WC6NbzriyewSpludxKY6h82OoBaGoUx7fh6qL7zmazffQYUfBdxj4VISDEqzC5rrKpeRhrrsWnkq2l7wpgwbYOtanIkx89JbP5D8B+0s87toDAAA=)

```kql
let Pieces = datatable(Emoji:string, Part:string, Order:int)[
    '🇦🇺', '==', 1,
    '🇧🇬', 'QZ', 2,
    '🇨🇦', 'yh', 3,
    '🇩🇪', 'Hc', 4,
    '🇪🇸', 'uV', 5,
    '🇫🇷', 'HI', 6,
    '🇬🇧', 'id', 7,
    '🇮🇹', 'mZ', 8,
    '🇯🇵', 'oh', 9,
    '🇰🇷', 'FI', 10,
    '🇲🇽', 'lJ', 11,
    '🇳🇱', 'Xd', 12,
    '🇳🇿', 'nJ', 13,
    '🇵🇱', 'WY', 14,
    '🇷🇺', 'uB', 15,
    '🇸🇪', 'yZ', 16,
    '🇹🇷', 'mh', 17,
    '🇺🇸', '2V', 18
];
print OriginalText = translate(
    'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ',
    'nopqrstuvwxyzabcdefghijklmNOPQRSTUVWXYZABCDEFGHIJKLM',
    base64_decode_tostring(
        reverse(
            toscalar(
                Pieces
                | order by Order asc
                | summarize PartsList = make_list(Part)
                | extend encoded = strcat_array(PartsList, '')
                | project encoded
            )
        )
    )
)
```