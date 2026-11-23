# Query Desk

AppADay 200, the milestone. Live at https://augustineiacopelli.github.io/appaday-200-query-desk/

Query Desk is a full data workstation in one browser tab. Load CSV files into a real SQLite database, find how tables connect, ask in plain English or write SQL, chart the results, and export a finished report. A forty exercise SQL course is built in. Plain Ask sends only names and three sample rows.

It assembles the six daily builds of Days 194 to 199 into one shell with one open project.

## The seven tabs

| Tab | From | What it does |
|---|---|---|
| Load | 194 CSV Intake | Reads CSV files into tables, types every column (ZIP codes stay text), offers one tap type changes, coercion of near misses and a 20 row preview |
| Relate | 196 Key Finder | Proposes primary keys and relationships with reasons, lets you confirm or reject each, draws a draggable diagram and writes the JOIN between any two tables |
| Ask | 197 Plain Ask | Turns a question into a read only query with Claude, lists its assumptions and shows exactly what will be sent before it is sent |
| Query | 195 Query Bench | Schema panel, SQL editor, result grid, history, saved queries, CSV export, and an Allow changes switch that is off by default |
| Chart | 198 Result Charts | Picks the chart that fits a result's shape, with overrides, a board of pinned charts that rerun on open, and PNG export |
| Report | new | Collects notes, saved query results and pinned charts in order and exports one self contained HTML file that prints cleanly to PDF |
| Learn | 199 Query Clinic | Forty graded SQL exercises on a practice college database, kept in its own project |

## How the tabs hand work to each other

A table card in Load opens in Query, and two or more tables bring up Find connections. A JOIN from Relate opens in Query and runs. Confirmed relationships go with every question in Ask, so Claude joins tables the way you confirmed. An answer in Ask can be saved, charted, opened in Query or added to the report in one tap. Any Query result can be charted or added to the report, and a saved query can be explained in Ask. A chart can be pinned and added to the report. Everything happens in the same tab, and the back button moves between tabs.

## What leaves the browser

Only Ask sends anything: table and column names, confirmed relationships, up to three sample rows per table (Settings can make that none), and the question. The What will be sent panel shows the exact text first. Every query Claude writes runs read only. The Claude key comes from the AppADay key ring and stays in this browser.

## Where data lives

Projects are standard SQLite files kept in IndexedDB on this device. Download saves a .sqlite file you can open in any SQLite tool or on another device. Projects saved by CSV Intake, Query Bench, Key Finder, Plain Ask and Result Charts open here, and projects saved here still open in those apps. The report is stored inside the project, and Export writes a separate HTML file with the charts as images and no scripts.

## Tested

Chromium at 375 by 812 with the iPhone user agent and at 1280 by 800: the full flow from three CSV files to an exported report, the Ask links with a mocked model, the read only and changes guards, Learn mounting and unmounting, reload persistence, a project file from each daily app, a 9 MB CSV at iPhone 13 size, and a 16 MB file refused, 91 checks in all. WebKit could not run in the build environment, so Safari is covered by a hand pass on an iPhone: the bottom bar under the home indicator, the type chips, the diagram drag, Ask with a real key, and printing an exported report to PDF from Files.

## Source

The shipped file is one index.html. It is built from parts in the appaday-194-csv-intake workspace with `node tools/build200.js`, and the shared Query Desk modules (core 1.3.0, keys, clinic, ask and charts) are filled in by `node tools/vendor.js apps/200/index.html`. Edit the parts there, never this file.
