[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA4VW34%2FaOBB%2B568Y5SmpCD%2FabR%2BoqFRV6p3arrS602kfqgqZZEhcnDiyHVjau%2F%2F9xjYxhoU2qxXYfPPNN%2BPxTKZT%2BNRrA%2B9baWpU8JkWEv5kxZYW2Bp1gFThZgG1MZ1eTKcVN3W%2FnhSymTa8UFLLjZl%2BJ6uceYp8ayny2lFko%2BkUPsi2wM4s4CNvSyAMNJJcdkqu2VogaPKDBIE9cYPusOAbjiVow5QBRjZI%2F3upSg28BQYbrsgfrUnjPVNbuSPGEoV19r43tVQLgEcuBGcN3Bd%2FyL6qId37jaao7NpGkI0EGqjQ3JOeL3yL4vD3UcujlbKE1Ll6JFcLbRRvq7FgZ%2Bvs5wjosTxrXinyt4SSGfqjyNKNks1qH1mDkedrnwQuuDksFDKRgeP76j%2Fsk9jzScb%2B%2BzHHbjmbvBlfR20oz8fvhHp5A1UwU9THxTnqQSDT6H664Lq7gTrninVFihNXXAH1%2BgbqAZW4rj5GlewwgH6B8lXogbPJPEJFcSUED1zzySxCRXH9AhXFdeHx9Q0UPnVCKo%2BbTV7dQPV6YHp2QqccXXi8u4EqcYdCdg54fkJRJhPehhAvYoyiv%2FD48gbK1Bw34bTvbqDWdL%2B5%2BR0XNRq5vVqrkeKkY4qV3NdkUP%2FtrfswUhdMMJUGU39fw%2FJfaNgWc9rraggXF%2FL83XBpXX9atdRpVrxcuh3b3ejaGqSu5C17TffaNbln%2FA6QN7akoDgUAvUyaWWLCaSu1WX510K2LRaGy1a%2FmE8m89m3%2FF1aoja8ZXY3C3R7KnH0LXLipCyXEJqVa5qRWUAM3SvQUP%2F5Tg5dwNS6TnzUmphrgQ3r0khWaGHZGPbIq9roa6Cor2XWxLbFSz2UvL%2FQ9IpauhAgNy5rlJDcJofTaTkJGtL5DGrZaZAKNrinqQJrNHvE1lmcBsZHG7%2BL%2FQvF6SdGlP8Qay%2FEgw%2BOKcUOK1JOFz3tqKxXbsc17mxs3Udh2ulS%2BgEmFa9oFLkwKDi75dLlrCOX%2BGTs7AoTzmZYka%2FBzVHJOIEkAz8qd0hD75zQumAnEj874sLd5azrxOGolLwMkmULp4K3j%2B6bhin%2BA6Hom17QaezwcbCirpQSIBWySo204yj1RBk9LvyOcvjEG1vwZG14Z8%2FJnqg9vugUg%2F%2BzXSwr1L7UtOwVhUKBRWURlGZRcCfFTFWrhj2ll8rHL5y4B15snZuaNok0H2rQHELurlRDSOupHO3rjC8tl%2BlB%2Fu94s9F%2Fb0cdWRh4%2FkLxT0tvK3S8RMkIYS%2FNzReP01vH8jixh3u7HHpv9j9IaS5OuQkAAA%3D%3D)

```kql
// Just Another Kusto Hacker entry (ref: https://github.com/microsoft/just-another-kusto-hacker)
// Concept: Find the most probable sentence with specified start and end words in a first-order Markov model
// Author:  ***
let getMostLikelySentenceWith = (firstWord:string,lastWord:string){
    let bigram = datatable(from_word:string, to_word:string, probability:real) 
    [ 
        "Just",     "another",   0.6,
        "Just",     "find",      0.2,
        "Just",     "catch",     0.2,
        "Please",   "find",      0.4,
        "Please",   "catch",     0.6,
        "another",  "Kusto",     0.5,
        "another",  "Perl",      0.2,
        "another",  "day",       0.2,
        "another",  "hacker",    0.1,
        "find",     "the",       1.0,
        "catch",    "the",       1.0,
        "Kusto",    "hacker",    0.5,
        "Kusto",    "explorer",  0.3,
        "Kusto",    "user",      0.2,
        "Perl",     "hacker",    0.4,
        "Perl",     "developer", 0.6,
        "day",      "in",        1.0,
        "the",      "hacker",    0.2,
        "the",      "thief",     0.4,
        "the",      "bandit",    0.2,
        "the",      "crook",     0.2,
        "in",       "paradise",  1.0,
    ];
    toscalar(
        bigram
        | make-graph from_word --> to_word with_node_id=word // Create a graph using the bigram
        | graph-match cycles="none" (start)-[connections*1..10]->(destination)
        where start.word == firstWord and destination.word == lastWord
        project from = start.word, path = map(connections, to_word), weights = map(connections, probability), to = destination.word // Return all of the non-cyclical paths (10 hops or fewer) between the specified First and Last words
        | project fullPath = array_concat(pack_array(from),path), weights // Add the origin word to the path array
        | extend sentence = strcat_array(fullPath," ") // Convert the path array to a sentence string
        | mv-apply weight = weights on (
            summarize cumulativeWeight = exp(sum(log(toreal(weight)))) // Approximate multiplication of all of the weights of all of the edges from source to destination
        )
        | summarize arg_max(cumulativeWeight,*) // Pick the highest-probabilty sentence
        | project sentence // Return just the string of the highest-probabilty sentence
    )
};
print MostLikelySentenceUnderConstraints = getMostLikelySentenceWith(firstWord="Just",lastWord="hacker")
```