[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAF2ST2uDQBDF736KwZMWDfTQS4qB3kpD6bGHEGRcx2iz7srshjTQD99149/gQX3vjTvzGyVZkPSbixobZSCDEq27CklRxbrNLXG7NZYbdUrA6vW7IWVJCRqEGIIDBADhp2YKEwg/Lsb2d6YyTHpjFN6UtjXxyltoexfT7mFw/TdHLXxHcV6UenPWvhStrUEYWyrkhQZnlPZ0KzRy+WAv5W9kbjRPieD4CoF06Hoca2orQF3NaGhbaC0nOAMDyxdKFm1UKA09gJgy9yHmyAhjCswNzqEJypRajORjboxgsfzgD1o8U3pi7GqY1g9puhtXD9fG1sPUWvkHV+UL0hatqEHchCSTKa0IImORbZwe5kOenjebl2O6i0iVsevp6iYl8LmNPyDLBiSAqgSXmuWegivpWP+Q8L9tI1Dmd8huCY66QJs7FHiLWuyiRiniXOmSTDS3ECfQVFV0L0v8DG6vYez0EMI4+AeKSSlnEwMAAA==)

```kql
let lex_chains = datatable(from_term:string, to_term:string, sentence:string) 
[ 
  "More", "Just", "red",
  "Just", "Another", "red",
  "Another", "Kusto",  "red", 
  "Kusto", "Hacker", "red", 
  "Hacker", "One", "red", 
  "One", "More", "blue", 
  "More", "Keyboard", "blue", 
  "Keyboard", "Warrior", "blue"
]; 
let terms = datatable(term:string, phrase:bool) 
[ 
  "Just", true,
  "More", false,
  "Another", true,
  "One", false,
  "Kusto", true,
  "Warrior", false,
  "Hacker", true,
  "Keyboard", false
];
lex_chains 
| make-graph from_term --> to_term with terms on term
| graph-match cycles=none (start)-[lex_chains*1..5]->(end)
  where start.term == "More" and end.term == "One"
  project lexical_phrase = strcat_array(map(inner_nodes(lex_chains), iff(phrase, term, "")), " ")

```