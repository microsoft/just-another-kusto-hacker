[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA1VOXUrDQBh89xRLXnaDURBE6EOhF%2FAEtSxfko8QmqRhdytBvICShz70oYgYBEGhP0fomXKEzrZF9GGY75tvZnZrk1dO0FD23eql7xa7vltuwFtgD%2B0N%2FA389F3rtU%2FgA1jDh3v7Cg8yC2SWuLfe53XvQ3b1jvkLQKZdy4tnwY3jKsWLGAwlTlNRKKmuQxkJCmEoH6%2B4qcl7%2FtrtPLYOn81UTJbvbjVXySxl7WZnGZSQU5Ji1FLq6VgZRuJm4IvtvCzJ5E8s7tlaynhouC4oYW0440b93357S5qyLnLr1LFrJMfjIHqYTFAeBCfh0i9SyPAAsH8yaE4BAAA%3D)

```kql
print a='😉🐮🔬🐭🐾😚🐧🐨🌭🐡🐞🐫🔾🌊😮🐬🔭🌨🌾🌡🐚😜🌤🌞🌫'
| extend a=extract_all('(.)', a)
| mv-expand a
| extend a=substring(base64_encode_tostring(strcat('abracadabra', a)), 19)
| summarize Message=replace_regex(replace_regex(tostring(make_list(a)), @'[[",\]]', ""), @'[+]', ' ')  
```