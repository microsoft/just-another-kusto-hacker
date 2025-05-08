[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAGWR227DIAyG7/sUvgQpm6A5VF3Vp9juI5p4HSohESHSju8+A10OGhcG2Z/928aghxabvsUzQxvu9gkcKsN3XzugYwjw/egdnNOt7fWP5KcZGadLYtIjQJHOYL+imrfJ3p71JxKYL26P3fCiLia4WfSG45S9Imh4dX0HgsSB6hm0LElweABJLhyWsnPuN+C7R9umUGxdW8+W5tIrA50t2Zyv8sep65QLrcb4SDU6dcPa6NGz6OL3wSarwzbqYIYgM9a+r+cltB9WdboJ62iUUY7N03IS/Dnt4vq8k6SQfoKJR3EopDxIWUpZiTys8E7tN9SRECHDqaQoFipfU5EoNlWKrVY5axG55sptnYIExfEoxWFBqv9SFBxo+BhuFG2dhsti89Hm0RbRltFW/Bc6D5vLhwIAAA==)

```kql
let decode=(encoded: real)
{
    let tostr = tostring(encoded);
    let substr = substring(tostr, 2);
    let chunkSize = 3;
    let tempTable = (
        range i from 0 to strlen(substr) - 1 step chunkSize
        | extend chunk = toint(substring(substr, i, chunkSize))
        | summarize chunks = make_list(chunk));
    unicode_codepoints_to_string(todynamic(toscalar(tempTable)))
};
let str1 = decode(0.074117115116032);
let str2 = decode(0.097110111116104);
let str3 = decode(0.101114032);
let str4 = decode(0.07511711511611132);
let str5 = decode(0.104097099107);
let str6 = decode(0.101114);
print strcat(str1, str2, str3, str4, str5, str6)
```