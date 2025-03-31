[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA2WUbW%2BjRhDH3%2FtTrPoG06NSgnHuLqepeqQyIU0tnX0HgTiyFtgC8bIQHmxA9%2BE7ix9CVSQEDDM%2F%2FvOfXTiryZ%2B0pgRIhJeaBpyRqR3dpqLWyF%2Bsu63qMhWxRlyWxkl9jDuUN%2ByWHF%2Bpk%2BcJweNaI0TJOkUj58PQNaL42YK6UQ7QRBZvItfZ2dai8e9MKIIrfJN4WcttK%2BJB5nTe06oIdEPRBqIuidHrmDhDYhzono8Fj3cmZ9aS%2B%2B6qt%2B9Xub82e2p97qI7U%2FfdhAeu03g6%2FJD5J%2BJMEg803F2Yxg0Srfk%2BgrVw%2BugrgFibB%2F8J1WXRdQBgLTr73kzC2bIAlBb74mEfrB%2FgRDQkMf9nrPEKiZGV2NYSwmyeANURr7f8WyVVegCxJ3axly3O6nzLqbIVPxHnklgVSSra6og1MKT0Pjz5nosoK%2BFhDBCa%2ByBrYW5bD3gmBUY6s%2FPdBUCPQh%2B%2Fu2eNN5LI8z2rzjKNj5JoW6sinK0AG6VPSxxJygDMK2qtZ2iF9Ql4Pz8ElgOA7Tuejx89ET9KYpDG720b13IyqK%2Fz1wbgFTUtkxDQgABnLTES0vnfAKSBJvZxZxbBmfhJEt8aWtb9CWqgtYp9v8Qck1qLV6o73RUAtX7EHuifEYDDQStSMwkg47XnttDjmpgh8eXLhOPK%2FhrHJYtpzSJc33KZT85yfxLW1kxEcol%2Fz3dMVJiBoZKG9ZZyPlWmm81BVYY9oJJRXbb%2FjbUFxdLppVYdva%2BaLKNl2jOyKNkbUsO8EfVUJUFH6vy4ZUaV5401IhwSVjISpIKW3bbNy%2Bno9pisDWysNXSV%2FE5mo%2BIorepUhDUZZ06%2BTN6tmPwkr3kqyC4VEaRCsLIR6VvDjv%2BBXJwFXSxa1zgVbOR%2FMsiHgT7I0MgjE5hkkF%2FJdOj8A7lWEVKU%2BStDPStWNbyWNge0YjfGNmJhHrHtxZOqCU53w%2B9FO3534KoS9G7s36yqaMwQVbKC05BtsTXWTv%2F7dAFndMe2HH2ZnjSoqPYPZfPLRsP5KkQZHp83zxh5eZEhRf0X4RirbxgFAAA%3D)

```
let Data = datatable (Id:int, Key:string, Weight:int, Value: string)
[
    1,  'my',         42, 'ZmFaWdo==udGludWVkIGFuZCB=pb0aWdhYmxlIGdlbmVyYXRpb24',
    2,  'dj',         43, 'gb2YZGdlLCBleGNlZWRzIHRoZSBzaG9ydCB2ZWhlbWVuY2=Ugb2Y',
    3,  'wack',       46, 'G5vd=SnVzdA==nSBwZX=pbmd1b==GFyIHBhc3Np=b24gZnJvbSJ=',
    4,  'of',         40, 'dGhIGN=cm5h=a25vd2xlQsIHRoY==gYnkgYmFuY2=Ugb2ZGVsmRl',
    5,  'sphinxs',    45, 'zZ=XZYW5vdGhlcg==cBvbmx=5IGJ5IGhp==cyByZWF==zb24LTW=',
    6,  'loves',      47, 'zIGRpc3R=md1aXNZCBie==B0aGS3VzdG8=lz5wbGV==hc3VYZg==',
    7,  'big',        41, 'gYW5yZS4=YW55IGNhc=m5hbCB=wbGVhc3VyZQ==JvbSBvdGCBpb=',
    8,  'quartz',     44, 'IHNpb=BaGFja2Vy0==aGUgY=29Bvd==GhlciBhb=mltYWx=zLCB3',
];
let Aggregated = Data
        | extend KeyTokens = extract_all('(\\w)', Key) 
        | mv-expand (KeyTokens)
        | summarize Freq = count() by tostring(KeyTokens), Weight
        | where binary_xor(binary_xor(Weight, Freq), 42) > 3
        | distinct Weight, Freq
;
Aggregated
| join kind=innerunique Data on Weight
| extend Start = binary_xor(Weight + Freq, 42), Len = 4 * (Freq + 1)
| project Results = base64_decode_tostring(substring(Value, Start, Len))
| summarize Message = replace_regex(replace_regex(tostring(make_list(Results)), @'\"\,', ' '), @'[\[\"\]]', '')
```