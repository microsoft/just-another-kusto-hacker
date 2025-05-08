[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA52QQWvDMAyF7%2FsVYlBkM3essGuh5zU599CUoGWaE%2BrYwVZGMvbj546O5bBdJl2EeHzvSUPsvEDJKZFl2AI%2B0b4d%2FUgppEZEztAGBoaY%2B6vw5gN4EvYvUGZ9HiM1UpNzCtW9RvMN0z%2FCYhvJW1YPBihGmmvH3kqrSr3eGNhclP3bmqeBLlQDBUgAmQcOr8oFbxeoQ%2FYsVo95kca%2Bp9i9MyziRx4cNVxHtjwpCUnyfVb1dObadUmypTaww2N1rG4rU51OOTCihucZDv%2BHXi%2F%2BHb142B%2FI697sUFWg79AgoP4EBHKS05oBAAA%3D)

```kql
print Message = 'JaKhunuasosctttk hoe e r r      '
| extend M = extract_all('(.)', Message)
| extend L=range(0, array_length(M)-1, 1)
| mv-expand M, L to typeof(long)
| extend W = L%4
| summarize  Message = replace_regex(tostring(make_list(M)), @'[\[\"\,\]]', '') by W
| summarize  Message = replace_regex(tostring(make_list(Message)), @'[\[\"\,\]]', '') 
| extend Message = replace_regex(Message,@'(\ )+',' ')
```