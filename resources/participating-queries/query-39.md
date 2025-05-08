[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH2S3U7DMAyF7/cUVq7aEaT+DMGExosgVHlttlm0TZWkEiAeHifZ1k5T2UWS2t85sTO3ygH1w+hgBwJRIxCR1rxqpLByRFNcQiAgmvQ1iSEbpbxFHDEQd1ZRGQ1xsmWdDyPeWInXVcv1eXoHRg0t1qqyzlB/TP7/DC1JoYUUmUilID7k/oB8KEQajfdoVVm1ZH33dmjJJXyXBAGeMNgfFRAcjO4gA6cBjcHvqlX90Z2SSZw+5mCdGiBf/YL6cqpvojW7TtQ7fUzpJuOc09S7xI77c9GBlZBJyNNUruDya/JlOL+Di2W4uIN9iUSHhDluK3IpvAHDCx5l9IDsxmez4LNZ9NlcfaZXYan/I+YesydT9fmSgO28Q5Oti2d44Bdab/1WrEu/lSDn4BME8iWPZFQUUVFGxSYi20iEUJHOLq9PaLB2ynAJY0+1blTll8E3ZyunL4PHVXqZHbsODf0oHls7ti62VaOrwgwlHX6qMBXJ1ZnfQoj0D5VZEIyQAwAA)

```kql
let input = "aaoa iiioo iioai iioaa ioia ioiai iiooa iioio iioaa ioaia ioaoa iioao ioia aaio iiioo iioai iioaa iioio ioia ioaia ioiai ioaoo ioaaa ioaoa iioao";
let oia = replace_string(replace_string(replace_string(input,"o","0"),"i","1"),"a","2");
let base3_list = split(oia, " ");
range i from 0 to array_length(base3_list)-1 step 1
| extend base3 = base3_list[i]
| extend d0 = toint(substring(base3, 0, 1)),
         d1 = toint(substring(base3, 1, 1)),
         d2 = toint(substring(base3, 2, 1)),
         d3 = iif(strlen(base3) > 3, toint(substring(base3, 3, 1)), 0),
         d4 = iif(strlen(base3) > 4, toint(substring(base3, 4, 1)), 0)
| extend len = strlen(base3)
| extend dec = iif(len == 4, d0*27 + d1*9 + d2*3 + d3 , iif(len == 5 , d0*81 + d1*27 + d2*9 + d3*3 + d4 , d0*9 + d1*3 + d2))
| extend character = unicode_codepoints_to_string(dec)
| summarize result = strcat_array(make_list(character), "")
```