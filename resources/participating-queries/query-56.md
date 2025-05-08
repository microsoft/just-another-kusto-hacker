[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAK2UT4/TMBDF7/0Uc0GbQFqcP05i0B44ICGQOHFbcUiboY1InSj1sq60H55nZ7cqu1V2I9GqzsjO7z137JmWDXG95QNdU10ZfNctB/bDwFUb0dE/wxshROR+5AalVERuOAWY/Un3xNawrul7tWeoXX3SndnxcPVx0cLE9piLx9h0/Q+8jIl+aDTWEA2V3nJQwEPlGGwfLu5p/2fJtq8gagGROfbc/Qr8nhYnvyPoTXXgYEH4WFqzuWPW0KLVimIpQ2gKQe8oCAJL7502vaEkDOktLWMpoicgEE+W02QpnpOlJ5NCzPVMlN9tWjpyGRflBIuVAqF9qgHYaWRitjsQTypHpvkL5suL7jL2GjKbdr+QNSCOLGL/32Uy7Z5cMi/SUSKfbQ7EkconTRby9UlTY9JU+kpPVMoKr/r4sUa+3R5M91Ah686Ybj9RGEjQfy2MHPtO5Ixrkqa5vyZZNjdX/xxxnGcvXLCzMxbPcval2vw+tZUxaZ/RwaYaGN3QqYU9NCy60LG+4jSge6ubTj82qWhsj9HZ8UR0Zot0D9DggdpG82ZXDYbuGrOjoOUtFq53TV2zDv8Cck1e/GkFAAA=)

```kql
let edges = datatable(x:real, y:real)[000,000, 000,999, 999,999, 999,000] | extend Name = 'Another';
let xp = 1;
let topText = print x = range(70, 960, xp)
| mv-expand x to typeof(real)
| extend y = case(
    x between(70 .. 155), 900 + (((x / xp) % 2)) * -150,
    x between(155 .. 185), 900 + (((x / xp) % 2)) * -800,
    x between(185 .. 270), 900 + (((x / xp) % 2)) * -150,
    x between(290 .. 380), -1780 + (((x / xp) % 2)) * -150 + 7 * x,
    x between(380 .. 400), 900 + (((x / xp) % 2)) * -150,
    x between(400 .. 490), 3680 + (((x / xp) % 2)) * -150 + -7 * x,
    x between(510 .. 540), 900 + (((x / xp) % 2)) * -800,
    x between(540 .. 710), -520 + (((x / xp) % 2)) * -150 + 2 * x,
    x between(730 .. 760), 900 + (((x / xp) % 2)) * -800,
    x between(760 .. 900), 575 + (((x / xp) % 2)) * -150,
    x between(900 .. 930), 900 + (((x / xp) % 2)) * -800,
    999.0),
    Name = 'Kusto';
let bottomText = print x = range(70, 710, xp)
| mv-expand x to typeof(real)
| extend y = case(
    x between(70 .. 156), 250 + (((x / xp) % 2)) * -150,
    x between(336 .. 444), 575 + (((x / xp) % 2)) * -150,
    x between(540 .. 710), 1640 + (((x / xp) % 2)) * -150 + -2 * x,
    0.0),
    Name = 'Hacker';
let bottomEdge = datatable(x:real, y:real) [ 000,000, 999,000 ] | extend Name = 'Just';
union topText, edges, bottomText,  bottomEdge
| render linechart with (legend=hidden)
```