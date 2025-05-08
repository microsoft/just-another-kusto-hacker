[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAKWZ22rcSBCG7/0UIlcJzEJXH9RqFl8EEwgJJJDDlZkL40yCFx8GZ2ATyAPsE+wD7pOs/tJIcUpd7u5dmwmW9f/t6a9qSlWd692h21992113p92Tf/7+68nvJ9fjr3Y3+8N3/Op4/Wr8+dP324ubq8un5yfd+HVuNmZDG7Pd1FySvItfmO3J9tm0/sf1+qzY0MMVGi75++f673Prk3yH5uElPbqd6e6y/ofi+vOWmy6X9b/uLy532Rg8eIflH5f1nufWol8BZHes3TW/8nhTEU+SAaRieJf131bFs+FSxPNl/v2XV6jk8+J/5qNyd1n/XTufx6Mv+L+u+rz+9/XP2vk8fin4fLnYP/wLZnP8xv37i9svu+7+7s/u8/3dTUfd4a4L3dfDbt/RyY9u9+2wu/3U7c24wNXV56evzkfpb7Q9N9vTU9pM1XQzVdBn4yVJHeV1VupsXuekzuV1Xup8Tsd88LUPR/2I5uh4VN4f5R8L249Sp2x/kDpl+0nqlO2TkcLC/onaANAcsPelBHBSqCAgL4UKAwpSqEHopbAEITZCmMP2oQQhSaH2MTBSqECwJIUKBGulsADBujYIdo4bP6ULIGzIiTUYfU6sAYk5sQZlyIlLYFIbGDfH8nkBiiMpVIA4K4ValXRSqIBwXgoLEFxjoXRzDN+UIEQp1CAMUqhBSFKoPSuMFBYg+MZi6ee4vS1A8E4KFQjeS6ECwQcp1CD0UliC0FgsfW2x9LXFMtQWy1BbLENrsQyNxTLMcXtZgBCCFGoQeinUIEQp1CAMUliC0FgY+zluLwoQepJCBUJvpVCB0DspVCD0XgoLEPrWDnKO27sShCiFGoRBCjUISQoVCNFIYQFCbCyMcY5bTe8QXU6swIjZrkQBErNdiQYl25WUwDQWyzjH8nUJSpJCbcIwUqjAGEgKFRCDlcIChKGxWA5zDEtT1hCkUIOwmts0CKvBTYOwmtxKEBqLZZrjVhq0EkmhAiGtRjdt2FyNbgqEtBrdChBSY7FMc9xKvUOKUqhBWHUjGoRVN6KO3Kt2pDRumtah29Q2kmRqO0kyta0kmdpekkxrM0mmdfQ22RFOxZFyag3JcnpS8/Cg5eik5ulBlH3kFU9nGksnUW2jSVTbaRLVtppEtb0mUWuzSdRYQMnWzuFkawdxsrWTONnaUZxs6yxOtrGM0nKiclZEEaVSRTFIpYoiSaWGYjk6OatF4VpLqVt1L+oBppNKDcVymlLqsWg5Rik1WbQcoNR2WeRaS+lyolKax2g5UikNZORXM56Gwq+GPA2FX015ORQnP7r9/d0fu8sD/hdjvGngHV92fLnx5cdXGF892me0cHjK80OCCxJnKm+W/yb+gZogJ+gJBoLDwmF5bTgsHBYOC4eFw8Jh4bBwODgcHI7fDhwODgeHg8PB4eBwcHg4PBweDs87gMPD4eHwcHg4PBwBjgBHgCPAEXjTcAQ4AhwBjgBHD0cPRw9HD0cPR8+c4Ojh6OHo4YhwRDgiHBGOCEeEIzJaOCIcEY4BjgGOAY4BjgGOAY4BjoGjAccAR4IjwZHgSHAkOBIcCY4ER+IAThHkEBqOoeEgGo6i4TAajqPhQBqOpOFQGvYew8/eKQGmDJhSYMqBKQmmLJjSgPOAOBHITrnDXs4F4mQgzgbidCDOB+KEIM4I4pQgzglyU+Kxl9OCOC+IE4M4M4hTgzg3iJODODvGT8e/Z49BD84gAAA=)

```kql
let pixel = "█";
let empty = "";
let J = dynamic([
    [0,0,1,0],
    [0,0,1,0],
    [0,0,1,0],
    [1,0,1,0],
    [0,1,0,0]
]);
let U = dynamic([
    [1,0,0,1],
    [1,0,0,1],
    [1,0,0,1],
    [1,0,0,1],
    [1,1,1,1]
]);
let S = dynamic([
    [1,1,1,0],
    [1,0,0,0],
    [1,1,1,0],
    [0,0,1,0],
    [1,1,1,0]
]);
let T = dynamic([
    [1,1,1,0],
    [0,1,0,0],
    [0,1,0,0],
    [0,1,0,0],
    [0,1,0,0]
]);
let space = dynamic([
    [0,0],
    [0,0],
    [0,0],
    [0,0],
    [0,0]
]);
let A = dynamic([
    [0,1,0,0],
    [1,0,1,0],
    [1,1,1,0],
    [1,0,1,0],
    [1,0,1,0]
]);
let N = dynamic([
    [1,0,0,1],
    [1,1,0,1],
    [1,0,1,1],
    [1,0,0,1],
    [1,0,0,1]
]);
let O = dynamic([
    [1,1,1,0],
    [1,0,1,0],
    [1,0,1,0],
    [1,0,1,0],
    [1,1,1,0]
]);
let H = dynamic([
    [1,0,1,0],
    [1,0,1,0],
    [1,1,1,0],
    [1,0,1,0],
    [1,0,1,0]
]);
let E = dynamic([
    [1,1,1,0],
    [1,0,0,0],
    [1,1,1,0],
    [1,0,0,0],
    [1,1,1,0]
]);
let R = dynamic([
    [1,1,1,0],
    [1,0,1,0],
    [1,1,0,0],
    [1,0,1,0],
    [1,0,0,1]
]);
let K = dynamic([
    [1,0,0,1],
    [1,0,1,0],
    [1,1,0,0],
    [1,0,1,0],
    [1,0,0,1]
]);
let C = dynamic([
    [1,1,1,0],
    [1,0,0,0],
    [1,0,0,0],
    [1,0,0,0],
    [1,1,1,0]
]);
let gap = dynamic([0,0,0,0,0]);
range row from 1 to 5 step 1
| extend p0 = iif(J[row-1][0]==1, pixel, empty), p1 = iif(J[row-1][1]==1, pixel, empty), p2 = iif(J[row-1][2]==1, pixel, empty), p3 = iif(J[row-1][3]==1, pixel, empty), p4 = iif(J[row-1][4]==1, pixel, empty),
        p5 = iif(gap[row-1]==1, pixel, empty),
        p6 = iif(U[row-1][0]==1, pixel, empty), p7 = iif(U[row-1][1]==1, pixel, empty), p8 = iif(U[row-1][2]==1, pixel, empty), p9 = iif(U[row-1][3]==1, pixel, empty), p10 = iif(U[row-1][4]==1, pixel, empty),
        p11 = iif(gap[row-1]==1, pixel, empty),
        p12 = iif(S[row-1][0]==1, pixel, empty), p13 = iif(S[row-1][1]==1, pixel, empty), p14 = iif(S[row-1][2]==1, pixel, empty), p15 = iif(S[row-1][3]==1, pixel, empty), p16 = iif(S[row-1][4]==1, pixel, empty),
        p17 = iif(gap[row-1]==1, pixel, empty),
        p18 = iif(T[row-1][0]==1, pixel, empty), p19 = iif(T[row-1][1]==1, pixel, empty), p20 = iif(T[row-1][2]==1, pixel, empty), p21 = iif(T[row-1][3]==1, pixel, empty), p22 = iif(T[row-1][4]==1, pixel, empty),
        p23 = iif(gap[row-1]==1, pixel, empty),
        p24 = iif(space[row-1][0]==1, pixel, empty), p25 = iif(space[row-1][1]==1, pixel, empty), p26 = iif(space[row-1][2]==1, pixel, empty), p27 = iif(space[row-1][3]==1, pixel, empty), p28 = iif(space[row-1][4]==1, pixel, empty),
        p29 = iif(gap[row-1]==1, pixel, empty),
        p30 = iif(A[row-1][0]==1, pixel, empty), p31 = iif(A[row-1][1]==1, pixel, empty), p32 = iif(A[row-1][2]==1, pixel, empty), p33 = iif(A[row-1][3]==1, pixel, empty), p34 = iif(A[row-1][4]==1, pixel, empty),
        p35 = iif(gap[row-1]==1, pixel, empty),
        p36 = iif(N[row-1][0]==1, pixel, empty), p37 = iif(N[row-1][1]==1, pixel, empty), p38 = iif(N[row-1][2]==1, pixel, empty), p39 = iif(N[row-1][3]==1, pixel, empty), p40 = iif(N[row-1][4]==1, pixel, empty),
        p41 = iif(gap[row-1]==1, pixel, empty),
        p42 = iif(O[row-1][0]==1, pixel, empty), p43 = iif(O[row-1][1]==1, pixel, empty), p44 = iif(O[row-1][2]==1, pixel, empty), p45 = iif(O[row-1][3]==1, pixel, empty), p46 = iif(O[row-1][4]==1, pixel, empty),
        p47 = iif(gap[row-1]==1, pixel, empty),
        p48 = iif(T[row-1][0]==1, pixel, empty), p49 = iif(T[row-1][1]==1, pixel, empty), p50 = iif(T[row-1][2]==1, pixel, empty), p51 = iif(T[row-1][3]==1, pixel, empty), p52 = iif(T[row-1][4]==1, pixel, empty),
        p53 = iif(gap[row-1]==1, pixel, empty),
        p54 = iif(H[row-1][0]==1, pixel, empty), p55 = iif(H[row-1][1]==1, pixel, empty), p56 = iif(H[row-1][2]==1, pixel, empty), p57 = iif(H[row-1][3]==1, pixel, empty), p58 = iif(H[row-1][4]==1, pixel, empty),
        p59 = iif(gap[row-1]==1, pixel, empty),
        p60 = iif(E[row-1][0]==1, pixel, empty), p61 = iif(E[row-1][1]==1, pixel, empty), p62 = iif(E[row-1][2]==1, pixel, empty), p63 = iif(E[row-1][3]==1, pixel, empty), p64 = iif(E[row-1][4]==1, pixel, empty),
        p65 = iif(gap[row-1]==1, pixel, empty),
        p66 = iif(R[row-1][0]==1, pixel, empty), p67 = iif(R[row-1][1]==1, pixel, empty), p68 = iif(R[row-1][2]==1, pixel, empty), p69 = iif(R[row-1][3]==1, pixel, empty), p70 = iif(R[row-1][4]==1, pixel, empty),
        p71 = iif(gap[row-1]==1, pixel, empty),
        p72 = iif(space[row-1][0]==1, pixel, empty), p73 = iif(space[row-1][1]==1, pixel, empty), p74 = iif(space[row-1][2]==1, pixel, empty), p75 = iif(space[row-1][3]==1, pixel, empty), p76 = iif(space[row-1][4]==1, pixel, empty),
        p77 = iif(gap[row-1]==1, pixel, empty),
        p78 = iif(K[row-1][0]==1, pixel, empty), p79 = iif(K[row-1][1]==1, pixel, empty), p80 = iif(K[row-1][2]==1, pixel, empty), p81 = iif(K[row-1][3]==1, pixel, empty), p82 = iif(K[row-1][4]==1, pixel, empty),
        p83 = iif(gap[row-1]==1, pixel, empty),
        p84 = iif(U[row-1][0]==1, pixel, empty), p85 = iif(U[row-1][1]==1, pixel, empty), p86 = iif(U[row-1][2]==1, pixel, empty), p87 = iif(U[row-1][3]==1, pixel, empty), p88 = iif(U[row-1][4]==1, pixel, empty),
        p89 = iif(gap[row-1]==1, pixel, empty),
        p90 = iif(S[row-1][0]==1, pixel, empty), p91 = iif(S[row-1][1]==1, pixel, empty), p92 = iif(S[row-1][2]==1, pixel, empty), p93 = iif(S[row-1][3]==1, pixel, empty), p94 = iif(S[row-1][4]==1, pixel, empty),
        p95 = iif(gap[row-1]==1, pixel, empty),
        p96 = iif(T[row-1][0]==1, pixel, empty), p97 = iif(T[row-1][1]==1, pixel, empty), p98 = iif(T[row-1][2]==1, pixel, empty), p99 = iif(T[row-1][3]==1, pixel, empty), p100 = iif(T[row-1][4]==1, pixel, empty),
        p101 = iif(gap[row-1]==1, pixel, empty),
        p102 = iif(O[row-1][0]==1, pixel, empty), p103 = iif(O[row-1][1]==1, pixel, empty), p104 = iif(O[row-1][2]==1, pixel, empty), p105 = iif(O[row-1][3]==1, pixel, empty), p106 = iif(O[row-1][4]==1, pixel, empty),
        p107 = iif(gap[row-1]==1, pixel, empty),
        p108 = iif(space[row-1][0]==1, pixel, empty), p109 = iif(space[row-1][1]==1, pixel, empty), p110 = iif(space[row-1][2]==1, pixel, empty), p111 = iif(space[row-1][3]==1, pixel, empty), p112 = iif(space[row-1][4]==1, pixel, empty),
        p113 = iif(gap[row-1]==1, pixel, empty),
        p114 = iif(H[row-1][0]==1, pixel, empty), p115 = iif(H[row-1][1]==1, pixel, empty), p116 = iif(H[row-1][2]==1, pixel, empty), p117 = iif(H[row-1][3]==1, pixel, empty), p118 = iif(H[row-1][4]==1, pixel, empty),
        p119 = iif(gap[row-1]==1, pixel, empty),
        p120 = iif(A[row-1][0]==1, pixel, empty), p121 = iif(A[row-1][1]==1, pixel, empty), p122 = iif(A[row-1][2]==1, pixel, empty), p123 = iif(A[row-1][3]==1, pixel, empty), p124 = iif(A[row-1][4]==1, pixel, empty),
        p125 = iif(gap[row-1]==1, pixel, empty),
        p126 = iif(C[row-1][0]==1, pixel, empty), p127 = iif(C[row-1][1]==1, pixel, empty), p128 = iif(C[row-1][2]==1, pixel, empty), p129 = iif(C[row-1][3]==1, pixel, empty), p130 = iif(C[row-1][4]==1, pixel, empty),
        p131 = iif(gap[row-1]==1, pixel, empty),
        p132 = iif(K[row-1][0]==1, pixel, empty), p133 = iif(K[row-1][1]==1, pixel, empty), p134 = iif(K[row-1][2]==1, pixel, empty), p135 = iif(K[row-1][3]==1, pixel, empty), p136 = iif(K[row-1][4]==1, pixel, empty),
        p137 = iif(gap[row-1]==1, pixel, empty),
        p138 = iif(E[row-1][0]==1, pixel, empty), p139 = iif(E[row-1][1]==1, pixel, empty), p140 = iif(E[row-1][2]==1, pixel, empty), p141 = iif(E[row-1][3]==1, pixel, empty), p142 = iif(E[row-1][4]==1, pixel, empty)
| project row, p0, p1, p2, p3, p4, p5, p6, p7, p8, p9, p10, p11, p12, p13, p14, p15, p16, p17, p18, p19, p20, p21, p22, p23, p24, p25, p26, p27, p28, p29, p30, p31, p32, p33, p34, p35, p36, p37, p38, p39, p40, p41, p42, p43, p44, p45, p46, p47, p48, p49, p50, p51, p52, p53, p54, p55, p56, p57, p58, p59, p60, p61, p62, p63, p64, p65, p66, p67, p68, p69, p70, p71, p72, p73, p74, p75, p76, p77, p78, p79, p80, p81, p82, p83, p84, p85, p86, p87, p88, p89, p90, p91, p92, p93, p94, p95, p96, p97, p98, p99, p100, p101, p102, p103, p104, p105, p106, p107, p108, p109, p110, p111, p112, p113, p114, p115, p116, p117, p118, p119, p120, p121, p122, p123, p124, p125, p126, p127, p128, p129, p130, p131, p132, p133, p134, p135, p136, p137, p138, p139, p140, p141, p142
```