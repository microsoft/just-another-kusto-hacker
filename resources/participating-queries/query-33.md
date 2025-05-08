[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG2SYW+DIBCGv/sr7iNsSkRBdIn/o0nTGKe0JVMxStt12Y8fmGUT2yMh4XL3Pu8BbW3seu8koGvdzW/tfah71eBgDwHY+D2jfUSLPASWU5KnqwghSrJ8m8sYydYhbBn3U5k44HDDoEUINBWE0XWh7RWcFDz3EDQnsUdNbB0l3O99Aom4cO2JKDxDzqIQiSfKHCb2h2MOwzYWs0cMywqnmPCtIisSkhTUA9M0fRia2jJvQvbkwsRihzP/LpzvOPYoC8aa8Sn2RbeUlB9wcAi+ob9G9Th2d9iVUz2cJKIhcAxGg7mPUh+RGgwGPQBaPP2V35Q5V8rIXg2t/CyXHRotj8fS/bCVQKsv9uOtNFzMl76vJ/UloTlPpdGWgmwOLQrwAqO+oV0IiyzG8AoxoXjpxgG2tv/7L4NqdCsrt41OZ66MrmYzqeGE+vpDVp2aDbIYjIMfNsh8MwgDAAA=)

```kql
datatable (vals:dynamic)
[ 
    dynamic([-198, 481.8333333333333, -268.8333333333333, 64.66666666666667, -5.666666666666667]), 
    dynamic([19, 137.41666666666666, -75.95833333333333, 18.083333333333332, -1.5416666666666667]), 
    dynamic([-573, 1279.6666666666667, -772.0833333333334, 180.83333333333334, -14.416666666666666]), 
    dynamic([469, -725.0833333333334, 492.2916666666667, -133.41666666666666, 12.208333333333334]), 
    dynamic([174, -154.08333333333334, 100.29166666666667, -25.416666666666668, 2.2083333333333335])
]
| mv-apply X=range(1, 5) to typeof(int) on (
    mv-apply with_itemindex=index coeff=vals to typeof(double) on (
        summarize chr=toint(sum(coeff * pow(X, index)) + 0.1)
    )
)
| summarize unicode_codepoints_to_string(make_list(chr))

```