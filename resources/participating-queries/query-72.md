[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG1VzW7cNhC+71NM92QDcpz2Vhc5uEkLtzHSpHXQQ1EElDhaMUuRCn9W3qAHP0QveYE+WJ6k34zk2gEKA+tdiZz5+P0Mz8+HUqZ8cX5u9ubJmM/fm/2w8VxoMN2e0+8x2UzPaGNNwV/r+UQeXeSSXNidbv7YbH+uuZDJVAamzvQ9u8C0d9htyYWGLj3fUmLj3Uc8waLBWDJd5yyHYrw/kmU0xDupMKcYdiTdWpP5ybbZbN8Gy4lCpM6lro65mNBxpi5Wr/WMHV3BZgcMkeRfG3PWrb9FWWCdpXkwQBmOlPfOewGi56NZq9j4+e5vrGy9GfFuux2PuXBysWbK8nWknXelGxh1t1L5hrshuE7wNwrcx13WTi5YPC/AFcjlXLmR9dRWwQgQM7hquTM1839s+ByxNwu/SsOo6C+9p9gvJ1tPaw4AyRzIHCIIRLd+LRI+330qBHKOeFon1PQU3G4o1EIpPpsN4OMb5c6d9Y7GeHC8sPQqzqtMAuabpzS6UAsrnYlziYmJD5yORQu03MsTQTWaYHZgEcSsemvBXwJUNVRSZXoJe0Sa3UeT7HqKqQKbnir2PfZQceMi9Q2HzA3lmU1BqwYcWhprES3QOeFnHOnlm2vqa+iKiyFTVXuo7HBZGRohxBu8HxQRuhtdqh2usG7PxzYqHG8UNtjvTS4NwUc5SkFL3u0XCUMRUPd+UdrwCevuFsw/PDAj0u6ifNsJFHiqhuK8mvSx4ctxQgeb4kSaKXqdoq0K8sX3WvRXzYvWFM+sPrExrG6SIyKkUU0leJBBm8wI2jramTypYFCvQ1qVBuHadSobBD1ql5chztIDJSCooI+iHLqABl8Fj7L5oSLOeJEY8Sxf1nibpYKxB0mlROd1Qpgh241I8kphXJlp4sB2u6WiuflQOWvlTnjCNgMBwHfiKaayRnfkQYyJ4AugEHE0tp/v/iG+7Xgq9ELC0CcY4qebBjxFPYHxKGmR85on10mCF2eZveKk7CYJlYD7tgxwJCYWr/af0N8kwIHBdYXKyMItS0vwQUcuDx4X464jpLD3Ks2SyP9x+uK/WFOGPeHo5osIzcYvCVLPZzOrsHmMsQxnqYag2dVZtAyH0WCeKolTMi5jr55BoPfudpWVHg2yZYLp5ueYuG3SjKnBU1gGmVYI0T4EAMmF+TMgws3z4GDWyZsFTVBxka8SazcAxr2JyezMOgqW+It5M+TCBHNjo7Mw8G1R/kTRAZ+frFRokYcjvV/ulL1qfJ+ysGYwYy8qtfiBOZfhEymT19yMPLbC7d7ZfAE76vV0CffA4+swutIyMOMe/s8El8khck0Hd+Cv6IzaIz2Pk/OxiO1o5O3mz+82j27EzV8wobr8R5dyuWaZULgmc22Xm1FvyYaeNvT1KWF1ruNoEm5AukZ26BlW4Y54Z1IyRzoZ4f13Hi9OHpU7bYD+9F9uwaIGoQcAAA==)

```kql
//https://aka.ms/jakh
let hackerWords = 
datatable(Word:string)
[
"Just as the caffeine kicked in, Alex realized he had accidentally deleted the wrong database.",
"Under no circumstances could he admit this to his boss.",
"So he did what any skilled hacker would do—he blamed ""mysterious system glitches.""",
"Technically, the logs did indicate an issue,",
" but that was because he had also disabled them.",
"All of this could have been avoided if he hadn’t stayed up all night binge-watching sci-fi movies.",
"Now, Alex had 20 minutes to restore everything before his manager checked in.",
"Only a true Kusto wizard could pull this off in time.",
"Tense, sweating, and muttering random KQL functions under his breath, he launched into action.",
"His keyboard clacked so fast, it sounded like an intense hacker movie montage.",
"Everything was going great—until he accidentally typed drop table ProductionDB.",
"Realizing what he had done,",
" he let out the most dramatic gasp ever recorded in office history.",
"Knowing there was only one solution, he quickly rewrote history.",
"Using advanced ""Pretend This Never Happened"" techniques, he created a fake report.",
"Somehow, no one noticed… except Dave from IT, who was already suspicious.",
"Taking a sip of his 9th coffee, Alex prepared for his greatest deception yet.",
"Only time would tell",
" if he could pull this off.",
"Hours later, his manager walked in and saw the smooth-running system.",
"Amazed, he praised Alex for fixing the mysterious glitch.",
"Celebrating internally, Alex nodded like a wise sage—while planning never to touch production again.",
"Kusto had saved him, but next time… he’d probably just ask Dave.",
"Even hackers need backup sometimes.",
"Remember, kids: ""Just Another Kusto Hacker"" knows how to survive! - by Copilot not me"
];
hackerWords
| extend FirstLetter = substring(Word, 0, 1) 
| summarize List =strcat_array (make_list(FirstLetter), "")
```