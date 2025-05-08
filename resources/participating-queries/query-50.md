[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJVT3W6CMBS+5ylOdiNNuoQq/i1hLzIX7LCbTAQCddPFB9ilJnMmS3w5n2RtqQgImSuN9Dvf+flOOU4oF89TwEx6BylP/PAFPRgg1ng8Vm84fn/KvdsXUb7LZolKRJ29nHZbBF/H3UbuuhTbotehkiI/NievCq/l8tyNUUZ2urKDS6722qpRxnH30yitru0G+775mmSFrKjeum1tPpSO/7MbcnYejTXM325pHAcrCJw0DnxuUgytUTIKWwh4BHwVs+jZ1GMHUQim+nxxEr0yj2efUqyp40WLkAvXQMRDC+GcoiVK9FYkvTK52xfJWYXcFsm0Qm5aSHFreJ+yhMEU7sHSFq0Wlk5MvZlLk4SuzDzTaS1C34smzJU/ceSHPHV55GatX3or9TRl5hQcB9odDH0bgwJkgIGQnkZtC2g4AU+eLQzDPoZOu9DIRUKqcnRlDuGbITsLVKBNBGXZJ0rU6XdPoC+jiEay2vCvakpXT4aJJAoQpXcmjx0tomq3pd3Sdutst6Syk78C5Kr61RSkQYqQmDvJxs9iCC642Rp09UU1KvB9MdtiUAY6ykIXbmULQuI/ky7mc5r4HwwSR4yHR7keqTmdMTfwU24uEYabG2T8AvAKJxy9BQAA)

```kql
datatable(a: string)[
    '     ██╗     █████╗     ██╗  ██╗    ██╗  ██╗\r\n'
    '     ██║    ██╔══██╗    ██║ ██╔╝    ██║  ██║\r\n'
    '     ██║    ███████║    █████╔╝     ███████║\r\n'
    '██   ██║    ██╔══██║    ██╔═██╗     ██╔══██║\r\n'
    '╚█████╔╝    ██║  ██║    ██║  ██╗    ██║  ██║\r\n'
    ' ╚════╝     ╚═╝  ╚═╝    ╚═╝  ╚═╝    ╚═╝  ╚═╝\r\n'
]
| mv-apply l=split(a, '\r\n') to typeof(string) on (
    project
        h=countof(l, ' '),
        a=countof(l, '█'),
        c=countof(l, '╗'),
        k=countof(l, '║'),
        s=countof(l, '═')
    | where h > 0
    | project x=pack_array(
                unicode_codepoints_to_string(
                    case(h == 23, 74, h == 18, 116, h == 20 and c == 0, 97, 32),
                    case(a == 15, 117, a == 14, 97, a == 21, 104, a == 16, 75, a == 17, 111, a == 0, 99, 32),
                    case(c == 6, 115, c == 1 and k == 3, 117, c == 1 and k == 4, 110, c == 0 and k == 0, 107, c == 0, 101, 32),
                    case(c == 0 and k == 0, 101, c == 1 and k == 3, 115, k == 0, 116, k == 4, 111, k == 3, 114, k == 5, 104, 32),
                    iif(s > 8, 114, 0)
                )
            ))
| summarize r=strcat_array(make_list(x), "")

```