[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI2UW2/iMBCF3/kVo74kkVIVaAGhqg8seym97KXde1UhN0zBJbEjx4GyZf/7HjtsYbfsBemLsD3j8RyfJGVLJ2Vhe0rbCZtT/NXHIpmyoSMKI3qo7e1RYlhYJlEkUlIm8lyqcS1Fpp85ryaq+NpDjfBzi2Wes+mLgrEyWiiRySS8CnpBHDwDffAcvAAvwStwDAbgBJyCM3AOXoM34C14By7AJXgPPoCP4BP4DL6Ar8F1dOjPEeZGKku9y/5ggGMYocYctltxtx43IlpSNtvl+1yo0SpkSXxvGcP+RDgFrC4sdhiHj81cVYG71G5dR5EvsqRSSa3+XLDbiRvN5v9WTPWcTfiXyt0OKv8snRt9x8m6otWoH/pRFPtNN89I2w7pEvabUfx7zwEFEXT8frjpAUXCGLEgfUswzMoTCTJFYtkUZJhzwwUrK6wreKsN7TiHIdVbjLzHaOJNtuNt5NL7esTFplM6BzE1Gh33aLlHO6b9Zozm3aDuHo3VdKPuQut+eFBFdVpPkn28W/Phbptu1w0661znGrRqSgWXK5mXqe+h8E0kWs3YWOd0aSESFYlIIZgTYpEzVaLRXNqJV2Ym0pLd6r+6h1platH6r7eyFqX21DW1R9tsu3esFmykSOU33gi90HNnST0fqjK7gcdc4B3yaCrV6EgqhfNtvtJ4n3GDfk9EajPC+s3C74MwV6XMMmFcFW+KITRIhA0zMeVhKgsbOktFcRBAWNjKCxZW/UbOV1XH278/YfQDnYm0U5wEAAA=)

```kql
let JustAnotherKustoHacker = () {
// create ascii mapping
let asciiMapping = () 
{
    let upperCase = dynamic(['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z']);
    (print ASCII = range(65,90,1) | mv-expand ASCII | extend Char = tostring(upperCase[ASCII - 65]))
    | union
    (print ASCII = range(97,122,1) | mv-expand ASCII | extend Char = tolower(tostring(upperCase[ASCII - 97])))
    | project ASCII = toint(ASCII), Char
    | union 
    (print ASCII = int(32),Char = tostring(' '));
};
// create an array of the ascii characters reepresentation for "Just another Kusto hacker"
let charCodes = dynamic([74, 117, 115, 116, 32, 97, 110, 111, 116, 104, 101, 114, 32, 75, 117, 115, 116, 111, 32, 104, 97, 99, 107, 101, 114]);
// run manipulations for converting it to scalar of type string with the value of "Just another Kusto hacker"
let result = print ASCII = charCodes 
| mv-expand ASCII 
| extend ASCII = toint(ASCII)
| serialize 
| extend Row = row_number()
| join kind=inner asciiMapping() on ASCII
| order by Row asc
| summarize array_strcat(make_list(Char),'');
toscalar(result)
};
print JustAnotherKustoHacker()
```