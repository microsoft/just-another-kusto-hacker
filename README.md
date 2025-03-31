<div align="center">
    <h1>Welcome to the<br><i>Just another Kusto hacker</i> ("JAKH")<br>contest!
</h1>
    <img src="./resources/images/kusto-logo.png" width="410px" alt="Kusto logo"/>
    <p><strong>Inspired by the <a href="https://wiki.c2.com/?JustAnotherPerlHacker"><i>Just another Perl hacker</i> ("JAPH")</a> challenge,<br> and <a href="https://www.ioccc.org/"><i>The International Obfuscated C Code Contest</i></a>,<br>you are invited
to participate in the<br><i>Just another Kusto hacker</i> ("JAKH") contest!</strong></p>    
</div>

---

Your challenge is to write a Kusto query that outputs the string `"Just another Kusto hacker"`. The query can be as simple or as complex as you like, as long as it is self-contained and can run on any Fabric EventHouse or Azure Data Explorer cluster.

You can use [a free Azure Data Explorer cluster](https://learn.microsoft.com/en-us/azure/data-explorer/start-for-free-web-ui) or the [Azure Data Explorer Emulator](https://learn.microsoft.com/en-us/azure/data-explorer/kusto-emulator-install) for testing.

Participants will have the opportunity to vote on the most creative and innovative queries across multiple categories, and the winners will be publicly recognized for their efforts!

## How to enter

1. **Create a Gist**:
    - Write a Kusto query that outputs the string `"Just another Kusto hacker"` and save it as a [Gist on GitHub](https://gist.github.com/).

2. **Submit your entry**:
    - Fill in the URL of your Gist in [this form](https://aka.ms/submit-jakh-query) and submit.
    - You can submit up to 3 entries.

For more details, refer to the [official rules](./CONTEST_RULES.md).

## Important dates

| Period | Starts                       | Ends                          |
|--------|------------------------------|-------------------------------|
| Entry  | April 1, 2025, 12:00 p.m. PT | April 30, 2025, 11:59 p.m. PT |
| Voting | May 1, 2025, 12:00 p.m. PT   | May 8, 2025, 12:00 p.m. PT    |

## Hints

The Kusto query language has several string transformation functions/operators that you may find useful while hacking, including:
- [base64-decode_tostring()](https://learn.microsoft.com/en-us/kusto/query/base64-decode-tostring-function)
- [extract()](https://learn.microsoft.com/en-us/kusto/query/extract-function)
- [extract_all()](https://learn.microsoft.com/en-us/kusto/query/extract-all-function)
- [replace_regex()](https://learn.microsoft.com/en-us/kusto/query/replace-regex-function)
- [split()](https://learn.microsoft.com/en-us/kusto/query/split-function)
- [translate()](https://learn.microsoft.com/en-us/kusto/query/translate-function)
- [mv-expand operator](https://learn.microsoft.com/en-us/kusto/query/mv-expand-operator)
- [parse operator](https://learn.microsoft.com/en-us/kusto/query/parse-operator)

## Have fun and be creative!

This contest is all about showcasing your Kusto skills and creativity. There are no prizes, but your hard work will be recognized. So, dive in, have fun, and show us what you can do!

For examples and inspiration, check out the [sample queries](./resources/sample-queries) and [this blog post](https://y0nil.github.io/kusto.blog/blog-posts/jakh.html).

***Good luck and happy hacking!***

---

**Creating a Gist**

  ![Creating a Gist](./resources/images/create-gist.png "Creating a Gist")

---

**Getting the Gist URL**

  ![Getting the Gist URL](./resources/images/share-gist.png "Getting the Gist URL")

---

**Submitting the Gist**

  ![Submitting the Gist](./resources/images/submit-gist.png "Submitting the Gist")


## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft 
trademarks or logos is subject to and must follow 
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.
