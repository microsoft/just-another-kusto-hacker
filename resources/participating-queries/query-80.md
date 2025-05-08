[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=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)

```kql
//////////////////////////////////////////////////////////////////////////////////////
/////////////////////////// Matrix multiplication in Kusto ///////////////////////////
//////////////////////////////////////////////////////////////////////////////////////
// Arbitrary NxA and AxM sized datatables (with values of type double) can be considered
// as matrices. These matrices can be multiplied to result in a NxM sized datatable
// as the product matrix.
let matrix_mul = (M1:(*), M2:(*)){
  let to_row_arrays = (T: (*)) { // Transforms any datatable "any NxM matrix" to arrays of rows
    T | project row_arrays = pack_array(*)
  };
  let to_col_arrays = (T: (*)) {  // Transforms any datatable "any NxM matrix" to arrays of columns
    T | evaluate narrow()
      | summarize col_arrays = make_list(parse_json(Value)) by Column
      | project col_arrays
  };
  to_row_arrays(M1)
  | project M1 = row_arrays, _joinKey = "#"
  | serialize 
  | extend m1_rownum = row_number()
  | join kind=fullouter (
    to_col_arrays(M2)
    | project M2 = col_arrays, _joinKey = "#"
    | serialize
    | extend m2_colnum = row_number()
  ) on _joinKey
  | extend m1xm2_ij = series_dot_product(M1, M2)
  | summarize M = make_bag(bag_pack(strcat("m", strrep("0", 5-strlen(tostring(m2_colnum))), tostring(m2_colnum)),  m1xm2_ij)) by m1_rownum
  | sort by m1_rownum asc
  | project-away m1_rownum
  | evaluate bag_unpack(M)
};
let m1 = datatable(a01: double, a02: double, a03: double, a04: double, a05: double)[
1.57, 0.62, 7.62, 1.74, 9.01,
7.2, 9.02, 6.9, 9.97, 7.84,
8.5, 5.9, 9.7, 1.13, 3.74,
4.53, 5.39, 5.89, 1.87, 7.33,
6.12, 2.9, 1.87, 7.9, 9.87,
2.82, 2.56, 3.92, 3.87, 9.34,
3.85, 7.8, 4.45, 4.76, 3.98,
4.66, 3.47, 3.45, 2.12, 8.12,
4.02, 6.96, 1.21, 5.23, 2.46,
8.12, 1.04, 0.69, 0.61, 3.15,
2.78, 4.32, 4.97, 1.22, 3.11,
3.93, 0.41, 1.98, 2.79, 4.01,
3.26, 3.92, 3.64, 2.87, 1.06,
2.31, 1.76, 2.73, 3.92, 1.45,
3.12, 3.31, 1.17, 5.22, 6.25,
2.25, 4.76, 5.85, 3.69, 0.7,
3.16, 4.98, 2.87, 4.87, 2.81,
1.58, 0.45, 5.06, 2.91, 3.71,
2.59, 2.83, 0.45, 0.94, 0.64,
0.6, 1.45, 3.13, 7.76, 0.28,
0.54, 8.51, 2.88, 3.06, 0.76,
5.37, 6.18, 3.26, 3.38, 3.48,
4.47, 0.6, 1.44, 2.78, 9,
7.87, 5.39, 4.3, 1.85, 1.57,
5.3, 2.73, 6.58, 3.26, 0.69
];
let m2 = datatable(b01: double, b02: double, b03: double, b04: double)[
0.56, 0.69, 0.49, 0.02,
0.13, 0.79, 0.72, 0.38,
0.78, 0.33, 0.19, 0.4,
0.49, 0.11, 0.16, 0.45,
0.03, 0.98, 0.73, 0.3
];
let m3 = datatable (c01: double, c02: double, c03: double, c04: double, c05: double, c06: double, c07: double, c08: double, c09: double, c10: double, c11: double, c12: double, c13: double, c14: double, c15: double, c16: double, c17: double, c18: double, c19: double, c20: double, c21: double, c22: double, c23: double, c24: double, c25: double)[
0.89, 2.28, 0.28, 1.24, 0.015, 1.45, 2.54, 1.34, 4.39, 4.69, 4.32, 3.76, 2.67, 5.55, 0.79, 1.17, 4.3, 3.25, 0.23, 5.94, 3.89, 0.38, 3.11, 4.32, 8.79,
1.24, 1.95, 4.5, 3.51, 1.57, 1.99, 2.35, 2.1, 3.45, 2.37, 2.74, 5.73, 1.65, 2.18, 6.78, 8.64, 3.69, 5.43, 4.32, 4.21, 2.69, 2.35, 1.61, 3.42, 1.65,
4.25, 1.29, 2.2, 3.35, 0.3, 2.4, 2.27, 4.3, 2.23, 5.66, 4.86, 4.56, 0.346, 1.45, 2.9, 3.29, 2.15, 5.71, 1.56, 0.05, 2.97, 1.74, 5.34, 0.86, 0.45,
1.52, 0.91, 0.45, 0.51, 0.02, 4.3, 3.12, 3.24, 3.98, 6.69, 1.23, 6.2, 0.02, 6.23, 0.85, 1.93, 4.85, 4.87, 2.56, 8.95, 4.8, 7.25, 3.52, 1.55, 1.4
];
matrix_mul(matrix_mul(m1, m2), m3)
// The result matrix is the product of the three matrices ((m1 x m2) x m3)
// The desired text appears in the diagonal of the result matrix (as the ascii numbers of the characters)
| project row = pack_array(*)
| scan declare (row_num:int = 0, diagonal:int) with (
  step s1: true => diagonal = toint(row[s1.row_num]), row_num = s1.row_num + 1;
)
| summarize diag_M1xM2xM3 = strcat_array(make_list(make_string(diagonal)), "")
```