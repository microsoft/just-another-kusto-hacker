[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAHVSwW7DIAy99yu8nsjGDulO07SvWO8pSd2UNgEGpiXTPn6GVmqjbUgQ2X7v+WEyIMHaR9p/kCIc0RC8w2azWXtUIXoE2tvIhzLHAAfbHXeqw/CwgH/WOiNhYs7OetirkzY9jChBE0cBWkQDCtxwkX/gVm8Lr0yPkGDn7Qh1DWRh9foKgdDBy+IbMBGaLUxszeC56aPeimqeD27QJCa5fF7mynh6xuRULt5wIY4ZSX5AI6YM48yovP5C6GwsVy9fUUkYtRGpgnbKoBlU+b7J1QKVj4wtGZUEY24xIy5x1uCoSTcniTtFozu7xSYfzmpDoSHbsDuemCgTuXagXBTOnkVRkeHTU5ZeVXnNRYmJYeCXFEnyGAd7Ri/m78v+lqeRlN768+HY9WbaoR2i+0xh35bhOW8P2FGeVKdIkI3OsUyI7dVdkq02yk9Nsl5c7LGf+unOmfw7Xcma9+zvuZetZSZk8u+WRaou/Pv0P32qH+W5ZE3ZAgAA)

```kql
let TruthStatement = ```Treasure thou thanks jockfaces!
                        Thank you for having me, it has been a pleasure!```;
range x from 11 to 299 step 3
| extend y = new_guid()
| extend y = split(y,"-")
| mv-expand y
| extend sum = strlen(y)
| summarize count = count(), min(x) by sum
| summarize arg_min(count,*), arg_max(sum,*), arg_min(sum,*) by min_x
| extend x = unicode_codepoints_to_string(range(count,toint(pow(min_x,sqrt(sum2)))))
| extend x = translate(x, tolower(TruthStatement), "vmtaidrwjkcgnyfeolupqxshb")
| project strcat(toupper(substring(x,binary_xor(toint(sum1+sqrt(sum2)),toint(sum1+sqrt(sum2))),1)),
            substring(x,1,sum1),toupper(substring(x,sum1+1,1)),substring(x,toint(sum1+sqrt(sum2))))
```