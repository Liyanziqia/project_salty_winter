Salty Winter: Did New York City use a record amount of road salt last winter?

This is a data journalism project I built as part of the Lede Program at Columbia University. It started with a simple question — we had a brutal winter, so how much salt did the city actually use? — and turned into a lesson in knowing when to stop digging.

→ Read the story 


What I found

New York City spread 504,811 tons of road salt during the 2025–26 winter season — the highest amount in the decade covered by this dataset, and roughly 90% more than the earliest season on record (2015–16).

To put that in scale: that is the equivalent of filling nearly 23,000 bulk delivery trucks, each carrying 22 tons of salt.

Salt use varied considerably year to year — dropping sharply in some seasons and spiking in others — reflecting variation in winter severity rather than a perfectly steady upward trend. The 2022–23 season, for instance, saw a dramatic drop to just 80,720 tons before rebounding.

Queens used more salt than any other borough in the latest season (153,925 tons), followed by Brooklyn (127,156 tons).


The data

Source: DSNY Salt Usage, NYC Open Data

The dataset covers 11 winter seasons (2015–16 through 2025–26) across all five boroughs. I fetched it directly via the Socrata API — no manual downloads.

ColumnWhat it meansdsny_stormStorm identifier (Storm 1, Storm 2, etc.)date_of_reportDate of the salt application recordmanhattan bronx brooklyn queens staten_islandTons of salt applied per boroughtotal_tonsCitywide total for that storm/report


What's in this repo

salty_winter.ipynb       ← the main notebook (analysis + charts)
df_salt_raw.csv          ← raw data pulled from the API (archived)
df_salt_winter.csv       ← cleaned data, grouped by winter season
df_season_borough.csv    ← borough breakdown for the latest season
chart_2015.png           ← truck pictogram: 2015-16 season
chart_2020.png           ← truck pictogram: 2020-21 season
chart_2025.png           ← truck pictogram: 2025-26 season
truck_icon_single.png    ← the single truck icon (designed in Illustrator)
salty_winter_scrollama.html  ← the scrollytelling piece


How I worked

Step 1 — Fetch: I used the NYC Open Data Socrata API (requests + pandas) to pull the full dataset as JSON and convert it into a DataFrame. No app token required for this dataset, though I signed up for one anyway as good practice.

Step 2 — Clean: The raw data comes in by individual storm event. I created a winter_season column to group storms spanning two calendar years (e.g. October 2025 through April 2026 = "2025–26"), then summed total_tons by season.

Step 3 — Analyze: I calculated year-over-year changes, borough breakdowns, and a per-capita figure (pounds of salt per resident). I also converted totals to truckloads using 22 tons per bulk delivery truck as the payload standard.

Step 4 — Visualize: I made two charts using Altair — a historical trend line and a borough comparison bar chart. For the pictogram, I designed a custom dump truck illustration in Adobe Illustrator (my son suggested adding a hydraulic support strut to make it more realistic — he was right), then used Python and cairosvg to tile it into three grid images showing the fleet growing across seasons.

Step 5 — Story: I built a scroll-driven narrative using the scrollama.js library, with the three pictogram images swapping as you scroll through the three time periods.


What I decided NOT to include

I originally planned to connect DSNY salt usage data to DEP reservoir chloride levels, to show where the salt ends up. I reached out to the NYC Department of Environmental Protection for comment and, after fact-checking, removed that angle.

The lesson I took from this: explaining one point clearly with one dataset, and knowing when a comparison is fair, matters more than adding more data.


Tools used


Python (pandas, requests, altair, cairosvg)
NYC Open Data Socrata API
Adobe Illustrator (truck icon design)
scrollama.js (scroll-driven narrative)
Jupyter Notebook



A note on the truck

The dump truck icon was drawn by hand in Adobe Illustrator — pink cab, taupe cargo box, blue salt scatter. My son, who loves trucks, reviewed the design and pointed out that a real dump truck needs a hydraulic strut to support the tilted bed. He was correct. Version 2 has the strut.


Questions or corrections

I reached out to NYC Open Data and the Department of Sanitation to verify the data. If you spot an error, please open an issue or get in touch.