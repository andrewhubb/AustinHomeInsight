# Austin Property Pulse (AUSTINTEL Austin Real Estate Insights)

**An interactive Power BI report that lets a home buyer filter 15,171 Austin-area property listings by price, location and school quality.**

**Live project page (Maven Analytics Showcase):** https://mavenshowcase.com/project/15998

## Portfolio summary

- **Business problem:** Buyers compare prices, locations and school quality in separate places. This report puts them in one view, so a buyer can narrow down properties near schools that meet their needs. An agent can also use it to check typical pricing for a property type or area.
- **Audience:** primarily home buyers; secondarily real-estate agents.
- **What the report contains:** a cover page and a main page with four views (Summary, Location, Schools, Features) switched with buttons, plus a property tooltip page. Users can filter by price, size, bedrooms, bathrooms, year built, school rating and other attributes.
- **Credit for the design:** I built this report by following the course instructor's design (see *Credits*). The layout, navigation and visual design are the instructor's. My own contribution is the build, this analysis and the documentation.
- **Live link:** the interactive report is embedded on the Maven Analytics Showcase page above.

## Key findings

These were computed independently from the CSV with Python (pandas). They are **not** outputs of the Power BI report. The figures are descriptive unless marked as model-based; they show associations, not causes.

1. **Location dominates price.** Among the 37 zip codes with at least 100 listings, the median price ranges from $204,200 (78725) to $1,140,000 (78746), about 5.6x.
2. **School ratings are much lower on the east side of Austin.** For listings in the city of Austin, 54% of those east of longitude -97.72 (roughly east of I-35) have an average school rating of 4 or below, against 18% in the west. The mean rating is 4.3 in the east and 6.3 in the west. The gap holds for other cut-offs (47% to 58% east, 18% to 21% west). The lowest-rated zip codes are 78725, 78721, 78724, 78744 and 78753.
3. **School rating looks more important than it is.** Higher-rated areas have larger homes: median living area is 2,816 sq ft for listings rated above 7, against 1,512 sq ft for listings rated 4 or below. The raw correlation between rating and log price is 0.45, but within a single zip code it falls to 0.14. In a rough regression with zip-code controls (model-based, R-squared 0.73), each rating point was associated with about 3.5% higher price. I used my own rating bands (4 or below, 4 to 7, above 7), which differ from the report's school-group slicer.
4. **Averages mislead.** Single-family homes have a mean listing price of $516k but a median of $410k. Vacant land has a mean of $785k and a median of $350k.
5. **Features look bigger in raw medians than they are.** A spa shows +44% in raw medians but about +11% in the regression above.
6. **Prices rose over the period.** Median price went from $385,000 (2018) to $434,900 (2020).

## Data and method

- **Source:** *Austin, TX House Listings* by Eric Pierce (Kaggle, v4, GPL-2). See `DATA_NOTICE.md`.
- **Scope:** 15,171 rows, all with a unique property ID (`zpid`). 15,020 are in the city of Austin. Sale dates run from 2018 to 2021 (83 rows are from 2021). This is a **historical snapshot, not current listings**.
- **Provenance in this project:** the course supplied the data as a resource. The CSV in `Data/` is identical to the Kaggle file.
- **Data model (Power BI):** a star-style model with `housing_fact` joined to `location`, `house`, `schools` and `features`, plus parameter tables for the slicers and a `_measures` table (for example Property Count, Average House Price, Median Home Price).
- **Data quality notes:** 106 rows are non-residential (vacant land, mobile homes, other). A small number of rows have implausible values (for example 47 homes with 0 bedrooms, 15 under 500 sq ft). I have not verified whether the report filters these out.

## Repository contents

| Path | Contents |
|---|---|
| `Austin Housing Data.pbix` | The Power BI report |
| `Data/austinHousingData.csv` | The source dataset (see `DATA_NOTICE.md`) |
| `Assets/` | Background images and navigation button icons used in the report |

## How to open it

Open `Austin Housing Data.pbix` in Power BI Desktop (Windows). If Power BI asks for the location of the data source, point it at `Data/austinHousingData.csv`.

## Known limitations and next steps

- **Key Influencers / Top Segments visual:** this visual relies on Azure Analysis Services / SQL Server Analysis Services and shows an error when the report is published to the web. A future version would recreate those insights without Analysis Services. Low priority.
- **Wording:** the report's cover text refers to "current listings". The data is a 2018 to 2021 snapshot, so the text should say historical listings.
- **Data cleaning:** exclude the non-residential and implausible rows in the model, or document the filters.

## Credits

- **Course:** *Microsoft Power BI Portfolio in a Day* (Udemy). The report design follows the course instructor's design.
- **Data:** Eric Pierce, *Austin, TX House Listings*, Kaggle (GPL-2). See `DATA_NOTICE.md`.
- **Built by:** Andrew Hubbard.

## Status

Completed. Last updated: 2026-11-05.
