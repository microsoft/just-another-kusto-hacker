[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH1VTY/bNhC9+1cQOkmFC68/sm0d+JCmu62TBlmsF2naIBBocdZiViIdktqu0/RSoNcAufWW/9Bflp/Q4YcsSklqw7BJPc6892Y4nkzI5ursgkxHFRhyruiuBmE0WRFGDb63FaS/SMXWbMmFGZMzUUgGbKmN4mKXjV6MCL6mY5JsxLM37MFqlYxJ+5pMSPKo0SZxoBmC1j+eN9v5pfzt+boFWhChQpoSlAfOLfDMTIv55e0gGnmM4aSHLVy8svx1Zqpih4kjWEmLGxvu5f3RJCicOYU/gOWvHkpxzXc9lX6r1elXS3YQtOZFpDPspH8kPtQTMKVkyTLZUg2nC+SbPKMVx7jwsKRKg0mWRjWA+5fwuuEK2DmHiulk+SLxztozwdfk5Z9ZTHruSJ8Jo+T+sBb7ZlCaDQBbCwZ3nrVdYvYGPlMfv5ODj5VrhObTZHwszeuGCtPUfcAsAGxJbvlWUcOl6EPmAWLLsSulNv3HCyzC6C2BOwOCtUp+orpEHSV+5bqks3un6ZF61qG9PQg8yuycWThnHkku0NCobY+/Ham35BUiyA0XbMWFADXwUoqQJKD3Sr6CwoTNY7uPY+IBiggMtz20LKkuRh29e1G3MYuw3AZsQ6AgNmAR5jspZ24jN9JXLg1csv6x0GRr/UAXnONpfn2dck3tKg0xszHxLXhNKw1tgN/xwsHg/BdsCHEifadO36aQqpMXq+2TfPKzQyJGUcHSjHxFpicn/59s3J6Ksn7jsl5iDFnzN86siEI/p0d9z6k+ph1WLoL0q/ety3Mlb0Bc8D1UWDYM0uXtZ3K4Tv9Alnsa9nRT11RhBGu71BtXWDyJFS6oyalS9JDW9AbyimuTuqNYvIQkWcTuO8fu6R78ddzgMGgGY8HAPkwE9/Az46CS1M6b7v77dmPxhQ9zjEU3nGoNNaZgvWt9RTsVaWJJ5jjUjp1r6WT2XvuWs0uyWpFFJ2l64v9/uKDV08bg3cR4Pf/7lrctp/cVN2lkZjDLg+vbr+FuT1v8J0Vw6S5Khffty0VwR7Ne3J5qLxfHXKRmSj5+ePdv+8HF+7+JagSpARuN1FQciOE12LYjB9kQgfMN7SI79AD/B4n3jeDksivFd6UJXfvxwz9/9YKPBn0w+nTkxa7iwEPao649j25jyjpFkePYluw/DA+oEiAIAAA=)

```kql
// STEP 1
let Fragments = datatable(WordId:int, Encoded:string)
[
    1, "SnVzdA==",         // "Just"
    2, "IGFub3RoZXI=",     // " another"
    3, "IEt1c3Rv",         // " Kusto"
    4, "IGhhY2tlcg=="      // " hacker"
];
// STEP 2
let DecoderConfig = datatable(ConfigId:int, Config:dynamic)
[
    1, dynamic({"DecodeMethod":"base64", "ValidateCharset":true, "RequiredFields":["WordId", "Encoded"]})
];
// STEP 3
let EntropyInputs = datatable(SeedIndex:int, SeedValue:string)
[
    1, "string_entropy_seed_1",
    2, "quantum_entropy_seed_2",
    3, "vibration_entropy_seed_3",
    4, "ghost_entropy_seed_4"
]
| extend EntropyHash = hash_sha256(SeedValue)
| extend WordId = SeedIndex;
// STEP 4
let JoinedFragments = Fragments
    | join kind=inner EntropyInputs on WordId
    | project WordId, Encoded, EntropyHash
    | order by WordId asc
;
// STEP 5
let DecodedWords = JoinedFragments
    | extend Decoded = base64_decode_tostring(Encoded)
    | extend CharsetIsAscii = iff(isascii(Decoded), true, false)
    | where CharsetIsAscii
    | project WordId, Decoded
;
// STEP 6
let ScoredWords = DecodedWords
    | extend MLScore = rand() * 100
    | project WordId, Decoded, MLScore
;
// STEP 7
let Randomized = ScoredWords
    | extend RandomBias = rand()
    | order by RandomBias asc
;
// STEP 8
let TokenPipeline = Randomized
    | extend Token = Decoded
    | project Token
    | summarize ChaosString = strcat_array(make_list(Token), " ")
;
// STEP 9
let OperationStatus = datatable(Step:int, Status:string)
[
    1, "loaded",
    2, "decoded",
    3, "validated",
    4, "assembled"
]
| extend Tag = strcat("STEP_", tostring(Step))
| where Step == 4;
// STEP 10
let FinalOutput = TokenPipeline
    | extend Words = split(ChaosString, " ")
    | mv-expand Words
    | summarize FinalPhrase = strcat_array(make_list(Words), " ")
    | extend Tag = "STEP_4"
;
// STEP 11 🎲🎲🎲 👅 run me as many times as you need to get the string in the right order 😂 🎲🎲🎲
OperationStatus
| join kind=inner FinalOutput on Tag
| project Output = trim(" ", FinalPhrase)
```