[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJVSXWvcMBB8v1+xFXmwwfH9gGBoKRSaECgl78dWt2frrA8jrXuXkh/flS2ngbQP9Yvk1czOzEr7PTwNFAlMAgQbGHRwLnj4QXwh8uCeIQZLgP6Y9xOmZIJv4fOA1pLv5URrmpiO7c4SC+Z7hnegvgI6OM+JpfERGUHQxhNFdVeQ39ZmGXy/4HxgMQMP8hNgQD2+gvUm96moZVIYxlut7mC/B9k2IMAEiWg3ReM3K7sXcD9v6TrlBDlKR1eOqPkgHStVtbVqVmQt0CmGM2legRwSS6e+4mDDhWKVq3WGnYPxMBp/7E6ztWFmcV3tQL5NumRbam8dlAH+1UTh1IW0edko7+yUA3FUg4zxxtKJ28V5dxNNP3BbEOI4UTRozS9aoj0i66HIfTEx8ZNx1C35PnRevK1RIUTY5Ev9j+YLXJaX889+WXV2DmNWfaSUsM8P4zWGLBplAjHic+VwpIM1iStzOlXvr1sHz2h82uw027reSaNU/fb+ilwXabKo6RCpp2tVqg18VOOsGlAPs/ov1jmT7lX9G5NCKP43AwAA)

```kql
// There is a lot common between my role and my passion. Challenge accepted.
let myRole = "I am just a data engineer";
let myPassion = "Just another Kusto hacker";
let challengeAccepted = "ohk-c"; // ohk, lets see
print myRole
| mv-expand role=extract_all("(.)",myRole)
| project role=tostring(tolower(role))
| join kind=fullouter (
    print myPassion
    | mv-expand passion=extract_all("(.)",myPassion)
    | project passion=tostring(tolower(passion))
) on $left.role==$right.passion
| serialize roleMatchPassionFirstTime=(role!=next(role) or  passion!=next(passion))
| where roleMatchPassionFirstTime
| summarize Message = tostring(strcat_array(make_list(iff(challengeAccepted contains passion,passion,role)),""))
| project Message=replace_regex(Message, @"ku", "Ku")
| project Message=replace_regex(Message, @"j", "J")
```