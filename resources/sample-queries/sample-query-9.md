[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA42Q207DMAyG7%2FsUVm%2BaQJBWxnFoaNfwCNtUpalZw3pSmrEJwrvjehswrmjlr4n9%2F6mdCj30xuk6r7CAKRTa00sboSe28cowkVkyn5jPzDWzYbZMx%2ByZnrlh5tg0FrOt7rMSHZ8no3kE9FwpSC8pRhQpxVgBLW8V3O0TtKfy%2Fb5yrdhDhqOeZWOWDRkFN5T7NgyVdBwtH6KfKaMAL7YpYDt0AhoeYQSda1%2FReOi0WYszOWiOqVKXeuqwq7TBzOEKd%2BJ059veO9usxGDOpJrFH%2BEzTBbFeVCximOpkjjhL1hLd4w777Txma4qMYsF6WSs%2FhwiqYH67QJ3naZOrf3Vj5n2m%2FwgHnoja9XS2lqpUvoH5%2FaWflPX2tl3hFqvMats74U5Ge5fcw2%2BzNBgyWIeFsugwnGeJE9UAon8AmKMIK1HAgAA)

```kql
let scrambled = datatable(a:int,c:int,e:int,h:int,J:int,K:int,k:int,n:int,o:int,r:int,s:int,t:int,u:int,bennie_was_here:int)
[
    4, 12, 10, 11, 13, 0, 7, 8, 11, 3, 2, 9, 13, 5,
    12,10, 11,  8, 13, 3, 0, 1, 6,  2, 9, 13,13, 13
];
scrambled 
| find where a > 0 project pack(*) 
| project haha=replace_regex(replace_regex(tostring(pack_),@"{|}|:\d+|,",""),'"',""), ii = extract_all(@"(\d+)",tostring(pack_))
| mv-expand ii
| project c=substring(haha,tolong(ii),1), haha, ii
| summarize make_list(c) 
| project replace_regex(replace_regex(tostring(list_c),@'\[|\]|,|"',""), 'b',' ')
```