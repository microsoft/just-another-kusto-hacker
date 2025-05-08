[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1UTW/bRhC961cMBAQhbUoiaYqUnKqH+lwgKHInKGolsaG4wnIVR3FzSWVXbhjE/QLUAkZqIOjBAdraRdFAKNqrEQSB2l+QEM5H06T+C5ldMrKKpkD2sNidmX1vZ/bNhoSDT0PKznsh4ZxAA2q6tVKzDduu16s16xxUKhwDoo7CvKilmDXDcqy6YzuGbldtVRUB8E4J2pSBiKC9DDAuICBa/UGMoK1h5PUCX9koIlRxFUqGaZaNFcOs21WnpjuW7mhQDD2OPssp25ZpmPqKXnOQzK5enbOsdwkjwCn0Q8/HRZdAl3iMS7LYxySQTC/rul59feQKpT3pbhGftoRfubCqrOFyVaSlqoWNAuAQIU06iFoiouuF7ffEZrVFB82QaOAPGCMRz/cqbICSm2AZ5uEqnAHFhKVFS+l0A1fPSa4Lcv4IepdKXr8fDoEhKVavQxRdA8vSwFBFlnzYJ7StBBFXgUagALnMCcI0A44HmkHksaEbd4M2d1nQ6XKZloYn8YTCVHEbU4MP6DpG50aoQFXVYI2GghIDqqDmt8mKK7DfBT235YSSI8PJWYUY/vcClqAwTEfVJMx8yMiM+m1gquabYaTAxOItYeoIA+C8zrPP6IfE59AXFUGMDqFubPokDF1OXR+flHmhK72K8MmVcGVByvwyUi6KUUPBaZnUyygp1EOmRDGWQBH5Lp+mXgLbwslUF7LKgKC+CORxjJJAFbNcFUCi/sunT5EDWYtAZm1xx2nMWYCtKwumFlB9fSZyfp/EsdcRvXD2eLyTjsZPpsnR1l9fHhxPPvt7c/to+8Xk4MnNuydbyVEilsnk4TS5N37x1Siz3kueTb5PP/4WrffHuESQf6bj+8mja7ce7l2b7T0YZ1gnm9sPkuzUy61kNkKspze+forLrZff7D9PJn98Phtnh57v7M1y2sfov/5s5/fjmz+e/Dqe4Q1+eHz97snmp38mZwsLTbMe8K4bcNILoha53DhPY1jreqKVBlEget0Vk3y92G0z2nPzcuTpL7aY/AqwxwrideNBr+ex4AqBtezHQMO/5RWSNqoLyVCftngbQX5GvIUKzSGIXUPOFbAKamHeRzlejkVZrtD/Yr9BzIv/tCbBl2BFtHhNSlywBNElepHkP50iLPhBtQgTOsJTzMcbc1k3UC5i1Ro9r4/fRcBD0iimu7cfHe6kP03Sg9/Sw+8gHd1JRz+noylu0tGNdPRJOrqF1v15CPpAeu6kh7eFIw/Z/SX9Yl/Mu1MELar46b0C6x962WkGAAA=)

```kql
let colorPalette = 80438616699584; //tolong(rand(281474976710656)); // <- for random colors
let focus = dynamic({"lon": -122.13129657807407, "lat": 47.642120308747465}); // <- where to place the heart
let scale = 0.0005; // <- zoom
let decode = (T:(Code:long))
{
    let bound = (halfBound:double, current:double) { (current + halfBound) % (2 * halfBound) - halfBound };
    T
    | mv-apply r = range(0, 44, 1) to typeof(int) on ( extend bit = binary_shift_right(Code, toint(r)) % 2, Row = toint(r / 5), Col = r % 5 )
    | where bit > 0
    | extend shiftRow = binary_and(binary_shift_right(Code, 45), 127),
             shiftCol = binary_and(binary_shift_right(Code, 52), 127),
             color    = binary_and(binary_shift_right(Code, 59),   7)
    | project point = geo_s2cell_to_central_point(geo_point_to_s2cell(
        bound(180.0, focus.lon + scale     * (Col + shiftCol - 64 - 2)),
        bound( 90.0, focus.lat - scale/2.5 * (Row + shiftRow - 64 - 4)),
        28)),
        tostring(color)
};
print Message = '䈐℈溌Ȇ锱䘑녉ȉ옱揸Ȍ옱挘ຌʈ아揸ʌ蘮⃠ຌ̈蘮䈐̌႟ࡂСΈ锱䘑Ό아揸톌Є옱獙熌І횪ꌘђЈ႟ࡂꐡЉ옱揸册Ћ萿䏰（Ќ옯勸Ҍ'
| mv-apply with_itemindex=Pos Char = unicode_codepoints_from_string(Message) to typeof(long) on
(
  summarize Code = sum(binary_shift_left(Char, 16 * (Pos % 4))) by Pos = Pos / 4
)
| extend Code = binary_or(Code, binary_shift_left(binary_shift_right(colorPalette, Pos * 3) % 8, 59))
| invoke decode()
| render scatterchart with (kind=map, title="❤ᲐⳘⱾⲦ Åℵ℺Ⲧℍℇ℟ KⳘⱾⲦ℺ ℍÅⲤKℇ℟ ❷⓪❷❺❤");
 
```