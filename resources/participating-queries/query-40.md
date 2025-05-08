[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAFVSwY7aMBC98xVTtBJBMhEJLNsWcdr20BakSru3VYVMMiFeHDuyDTRVP77P6e7CHhzFM2/eezNjzYEKa/VDOFYVrQatUybQhr2Xe6YVjYYPrSz4M4WaqVJGaqqcNUGxS+mxZs8kHffZk+1Q48lW/dUH6XytWvpqAjvwek7pW/BgOfGkY+moUd4ra0BuiX+32rpY5qSBtOEzna3TpV/GtGc+kD2GPq5VBVlT9pdCnZRWf2QA03/szupSd7S3dK4ZlMZSIw3V0iNmmHZcQenDkHYd3cs2SGXou2xg/TGlH8odRoO/8BMYChvMAL9OFmErtU5GSToeidcBjS/ANYC982QqMBInu61msw91shlPMkFZxDanCfqMzjcCFfAaupZtlaBrZfYR0jr7zEXo+YLFMpL1GHrLgcamDtwhXHZGNqpInvJZJrI5zuxW5PkCJxczREQ+xb/4JLKpyPC9E/l82iNzILNFDKHq7lYscvERtwUy8xmyc+DzX+PlyzuA3jvXUf9iGohrx/dWHxuTIeLZKYmd8GU8P61XcUNxSva8Ncdmxy6J5c9okg7KlCtlDLur1wj0jeYqpC/MtFrRjVP7OqTrK91XakwpalsX4mLfBKUvYvjYNNLBEn3hwpZcXp44Zl9IbDfuLGnkgbda+YC1CRoOrxt8X/kPdfdxFzoDAAA=)

```kql
let coolStuff =
print Message = '"Space: the final frontier. These are the voyages of the starship Enterprise. Its five-year mission: to explore strange new worlds; to seek out new life and new civilizations; to boldly go where no man has gone before!" by Captain James T. Kirk'
| extend M = extract_all('(.)', Message)
| extend L = range(0, array_length(M)-1, 1)
| mv-expand M, L to typeof(string)
| project L = toint(L), M;
let key = dynamic([231,141,135,226,222,3,14,20,22,9,10,19,17,240,141,235,169,171,175,62,89,161,243,234,192]);
print key
| mv-expand key to typeof(int)
| project Column1
| serialize
| extend Position = row_number()
| join kind=inner coolStuff on $left.Column1 == $right.L
| project Position, M
| sort by Position asc
| summarize DecodedMessage = strcat_array(make_list(M), "")
| project DecodedMessage
```