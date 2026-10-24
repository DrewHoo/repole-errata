# Corrections to Warren Repole's college football score and line files

Warren Repole's Sunshine Forecast site (repole.com) gave away one XML and one CSV file per season, 1978–2013, with every FBS game's date, teams, home team, score, site and closing line: `cfblines.zip` and `bowllines.zip`. The site is gone, and the files survive only on the Wayback Machine. They are the most complete free source of pre-2002 lines, so a lot of people still build on them.

While building [cfb-streak-king](https://github.com/DrewHoo/cfb-streak-king) I compared every game in the files against James Howell's historical scores and, from 2001 on, [cfbfastR](https://github.com/sportsdataverse/cfbfastR-data) and [CollegeFootballData](https://collegefootballdata.com). This repo is the list of rows where the file is wrong, plus the FBS-vs-FBS games it never listed. There is no upstream to send it to, so it lives here.

| file | rows | what |
|---|---|---|
| `repole-errata.csv` / `.json` | 79 | 60 wrong scores, 6 blank bowl scores, 11 reversed home teams, 4 wrong lines, 2 wrong dates |
| `missing-games.csv` / `.json` | 38 | games absent from the files, nearly all 1992–93 Big West, with Howell's scores |

Three rows were added on 2026-09-29: UT Arlington at West Texas A&M 1979, Navy at Delaware 1992 (the file has it at Navy), and William & Mary at Western Michigan 2003. All three involve a school that later left the top division. The first comparison couldn't match those schools' names across sources; once it could, Howell's pages disagreed with the file, and CFBD confirms each fix.

One row was added on 2026-10-24: Alabama vs Auburn at Legion Field, 1990. The file lists Auburn as the home team, but 1990 was Alabama's designated home game. Howell writes "vs." for every Iron Bowl in Birmingham, so the receipt is a quote from Wikipedia's Iron Bowl article, in the JSON row's `receipts`.

One game stays open. For Colgate at UConn on 2000-09-09, the file says 34–7, Howell says 37–7, and Wikipedia says 27–7. It isn't in the list because no two sources agree on a correction.

## How to read a row

Rows are keyed by `file`, `date`, `visitor` and `home` exactly as the XML spells them (`Texas A+M`, `S-M-U`, `UL-Lafayette`). `published_*` is what the file says. `corrected_*` is what actually happened. Scores are visitor–home. Lines are the home team's, negative when the home team is favored, so `-3` means the home team was a 3-point favorite.

`swap_home = yes` means the file lists the true home team as the visitor. When a game is both swapped and rescored, the corrected score is in the file's visitor–home order, before the swap. The two 2007-10-27 rows are one mistake: Iowa State–Missouri and Mississippi–Auburn were swapped whole, lines included.

`confirmed_by` names the sources that agree with the correction. Every score and home fix agrees with Howell, except Chattanooga at West Virginia 2002, which Howell's FBS pages don't carry, and the 1990 Iron Bowl, where Howell names no home team; from 2001 on, cfbfastR and CFBD agree too. Two of the four line fixes are the swapped 2007 rows. The other two come from cfbfastR's per-book closing lines, where every book disagrees with the file. CFBD's own neutral-site flags before 2005 were not reliable enough to use as a tiebreak, so no neutral-site corrections are in this list.

The JSON is the same data in the shape a parser applies: `score`, `swapHome`, `homeSpread` and `newDate` are the fixes, `published` is the file's version.

## What is not here

- Repole's files themselves. Get them from the Wayback Machine: [data page snapshot](https://web.archive.org/web/2022/http://www.repole.com/sun4cast/data.html). Consider [donating to the Internet Archive](https://archive.org/donate); without it these files would be gone.
- Neutral-site and off-campus rulings, which depend on how you define home.
- Anything after 2013. Use cfbfastR or CFBD.

## Sources and credit

- Warren Repole, Sunshine Forecast, for the files being corrected.
- [James Howell's historical scores](http://www.jhowell.net/cf/scores/ScoresIndex.htm), the reference every score fix was checked against. His site is copyright James William Howell; the rows here carry only the fact that a given score is his, not his pages.
- [cfbfastR-data](https://github.com/sportsdataverse/cfbfastR-data) and [CollegeFootballData](https://collegefootballdata.com) for 2001 onward.

## License

The data in this repo is released under [CC0 1.0](LICENSE). Game scores, dates and home teams are facts; the compilation is yours to copy, paste into your own dataset, or redistribute without attribution. Credit is appreciated, not required.

If you find another wrong row, open an issue with the game, the file's version, and a source that shows the correct one.
