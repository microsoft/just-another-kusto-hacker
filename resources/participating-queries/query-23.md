[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH2STUvDQBCG7/6KJQhJsT00iV5KwB5sUQ8eBIuWGsbs2KRNsmEz/cQf7+ymtamIl2Xn43nf2Y9KZyWJ+zKjDPJn4mguIuFslJb96GFV08Bs/eh1cr2W4zRP5lFkU0H0yFVl92EE49EC/Jedc/ElKtA1/pLcZJQeVR2xhrwvnIHTZPwm48dYJkqiPFWCphKcMmGTCY+9bIdbwlJaBZ78A2q8CWOJphyTqq2/19bvnEHhv1D4BzTM8wmPUjNYQbKMQWvYmeZ+105h18CuocGKdQ+3FTBpMKZ+BEgJ2lWoPr3GsWVytyUNCaE8MNjE3q3z7k2HvTfo7WdXnUunK9jV9Bi2XhUF6GyP4klL1A1s5ixgiXGe1eSd6bb8RlnJj4UlBwkywQMlQIeztdW6whWuASutFpiQmLrmmwgoFaWohf0VIuWLQe3OWOlM+RsuelhYbwIAAA==)

```kql
print InitialString = "word1=Just;word2=YW5vdGhlcg==;word3=Kusto;word4=aGFja2Vy"
| parse InitialString with "word1=" val1 ";" "word2=" val2_encoded ";" "word3=" val3 ";" "word4=" val4_encoded
| extend val2 = base64_decode_tostring(val2_encoded)
| extend val4 = base64_decode_tostring(val4_encoded)
| extend AllWords = pack_array(val1, val2, val3, val4)
| mv-expand Word = AllWords to typeof(string)
| extend ExtractedWord = extract(@"^([A-Za-z]+)$", 1, Word)
| summarize OrderedWords = make_list(ExtractedWord)
| extend FinalSentence = strcat_array(OrderedWords, ' ')
| project ['Just another Kusto hacker'] = FinalSentence
```