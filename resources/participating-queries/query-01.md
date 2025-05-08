[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAC2Oyw6CMBBF93zF7NomShBqy8aFJPIbpGkaRVvalMGg8eMdH3c1mZM5c1MeJ4TLCgdg8qj3utGyrtROnVSvpWrVXtd1JbsfUT2xlmijug9hxQvCfWtS8g+w5HArZmNxMN5zxstSsA3JBcQJeAGUeQnB5PHpIC6YFqSbYG5umJGKnPl39uOMHCMV47S2BjmrVhJZQSkE/Uw5Xp3Fv+MNHJATYsQAAAA=)

```kql
print hx = '4A75737420616E6F74686572204B7573746F206861636B6572'
| mv-apply c = extract_all('(..)', hx) on (
    summarize output = make_string(make_list(toint(strcat('0x', c))))
)
| project output
```