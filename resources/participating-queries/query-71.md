[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG2WzUsjQRDF7/4VQ04KQau/5mPBg0ggGDCg8bTsIZqgAY2QzbIK+8dv19SrmZ6eJJffq+5+XZPX07pZH+P3+X17/vWj2Hz+iTQtvnt8WR+3r5+HWPl9POz2rxc/z4r4uboq7p4eVy2bS5ra6eTOTKZ2jFbQDNEJkqAB+r7q+2oQNILtlk7Mn+I+ToZStII0xLiPH6MXNEMMglaw3TKIfoz7lD1q1QqaITqZm6EXJMEADH1Vt6zEfGXWk2mdcHUZWrZgk7EDE1gTu7lfruazBwmNxPAmPkTLJmMLpoS5znGZjHmOT+opB7AF675lUi/Ro8GhuedGcBIGzI0g+wE7MAmLGRJcsgHiHjAbhBPswDZjj7Vg2aTUXJ7jaJWKUlNSYXLhVBCEWCLqOfdaS08dx2Vz7rXJmOc7MAm3ZhY/94zfSJOw1i2YEo7GM4f5yjrHow6WTRDbAxsjqo65zsbuBDuwydhjbc4Bc0hYz/Ui3kRL6QRZLXgV8uw4OizYAZG1rPUSdRIWs0pvGX6WSu+ZgbAQNBL8PPVJ4SHMSAQICyFtNHrd8BVHiehHLIQZCYc1Y+EhCMI2KkI60l25OD0rXmcTNjjnAWwyLsEkLGY4AcsmDiLRARuKwp8UBsKOhIWBCj0f85vbBa49h/Dn3DkC75hfKO68ypjnl2ASFrNa71BuA/n2or1RuacmF+00B2FVdG4+HdGXzCP522jvTcJat2DK2GE+WMwQ4KKKg3hjO+b3oY6Mn7JlrTeok7CYIYAZ/9UMCWu9BFPCfK9UmK+sc2rUwbIJgntgAwTXMdfZoDrBNdhk3GBtznzYfKWXGE3Ofp39Kw7b/WZ7KN53++3L2/pwLP7ujm/F+ffHbn9N8f+lj/XXtb34D+VQE2ZMCQAA)

```kql
datatable(x: double, y: double, category: string)[
    // JUST
    1.0,2,"J1",2.0,2,"J1",2.0,2,"J2",2.0,1,"J2",2.0,1,"J3",2.0,0,"J3",1.0,0,"J4",2.0,0,"J4",1.0,0,"J5",1.0,1,"J5",
    3.0,2,"U1",3.0,1,"U1",3.0,1,"U2",3.0,0,"U2",3.0,0,"U3",4.0,0,"U3",4.0,0,"U4",4.0,1,"U4",4.0,1,"U5",4.0,2,"U5",
    5.0,2,"S1",6.0,2,"S1",5.0,2,"S2",5.0,1,"S2",5.0,1,"S3",6.0,1,"S3",6.0,1,"S4",6.0,0,"S4",5.0,0,"S5",6.0,0,"S5",
    7.0,2,"T1a",8.0,2,"T1a",7.5,2,"T2a",7.5,1,"T2a",7.5,1,"T3a",7.5,0,"T3a",
    // ANOTHER
    10.0,2,"A1",10.0,1,"A1",10.0,1,"A2",10.0,0,"A2",10.0,1,"A3",11.0,1,"A3",11.0,0,"A4",11.0,1,"A4",11.0,1,"A5",11.0,2,"A5",10.0,2,"A6",11.0,2,"A6",
    12.0,2,"N1",12.0,0,"N1",12.0,0,"N2",13.0,2,"N2",13.0,2,"N3",13.0,0,"N3",
    14.0,2,"O1",14.0,0,"O1",14.0,0,"O2",15.0,0,"O2",15.0,0,"O3",15.0,2,"O3",15.0,2,"O4",14.0,2,"O4",
    16.0,2,"T1b",17.0,2,"T1b",16.5,2,"T2b",16.5,1,"T2b",16.5,1,"T3b",16.5,0,"T3b",
    18.0,2,"H1",18.0,0,"H1",18.0,1,"H2",19.0,1,"H2",19.0,2,"H3",19.0,0,"H3",
    20.0,2,"E1",21.0,2,"E1",20.0,2,"E2",20.0,0,"E2",20.0,1,"E3",21.0,1,"E3",20.0,0,"E4",21.0,0,"E4",
    22.0,2,"R1",22.0,0,"R1",22.0,2,"R2",23.0,2,"R2",23.0,2,"R3",23.0,1,"R3",23.0,1,"R4",22.0,1,"R4",22.0,1,"R5",23.0,0,"R5",
    // KUSTO
    25.0,2,"K4",25.0,0,"K4",25.0,1,"K5",26.0,2,"K5",25.0,1,"K6",26.0,0,"K6",
    27.0,2,"U11",27.0,1,"U11",27.0,1,"U12",27.0,0,"U12",27.0,0,"U13",28.0,0,"U13",28.0,0,"U14",28.0,1,"U14",28.0,1,"U15",28.0,2,"U15",
    29.0,2,"S11",30.0,2,"S11",29.0,2,"S12",29.0,1,"S12",29.0,1,"S13",30.0,1,"S13",30.0,1,"S14",30.0,0,"S14",29.0,0,"S15",30.0,0,"S15",
    31.0,2,"T4",32.0,2,"T4",31.5,2,"T5",31.5,1,"T5",31.5,1,"T6",31.5,0,"T6",
    33.0,2,"O9",33.0,0,"O9",33.0,0,"O10",34.0,0,"O10",34.0,0,"O11",34.0,2,"O11",34.0,2,"O12",33.0,2,"O12",
    // HACKER
    36.0,2,"H4",36.0,0,"H4",36.0,1,"H5",37.0,1,"H5",37.0,2,"H6",37.0,0,"H6",
    38.0,2,"A11",38.0,0,"A11",38.0,1,"A12",39.0,1,"A12",39.0,0,"A13",39.0,2,"A13",38.0,2,"A14",39.0,2,"A14",
    40.0,2,"C1",41.0,2,"C1",40.0,2,"C2",40.0,0,"C2",40.0,0,"C3",41.0,0,"C3",
    42.0,2,"K7",42.0,0,"K7",42.0,1,"K8",43.0,2,"K8",42.0,1,"K9",43.0,0,"K9",
    44.0,2,"E5",45.0,2,"E5",44.0,2,"E6",44.0,0,"E6",44.0,1,"E7",45.0,1,"E7",44.0,0,"E8",45.0,0,"E8",
    46.0,2,"R6",46.0,0,"R6",46.0,2,"R7",47.0,2,"R7",47.0,2,"R8",47.0,1,"R8",47.0,1,"R9",46.0,1,"R9",46.0,1,"R10",47.0,0,"R10"
]
| render linechart with (ymin=0, ymax=2)
```