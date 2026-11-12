# Airbnb Market Analysis Dashboard

## Project Overview

This project explores Airbnb listing, host, pricing, and guest-review
data using Microsoft Power BI. The goal is to turn raw marketplace data
into an interactive report that helps users understand the size and
distribution of the Airbnb market, how property characteristics relate
to price, how hosts perform, and how guests rate listings.

The report is organised into four analytical pages, supported by a
separate KPI summary page:

1.  **Airbnb Market Overview** -- explores listing distribution across
    cities, room types, property types, and host-registration periods.
2.  **Pricing and Property Analysis** -- examines listing prices by
    country, local currency, room type, and accommodation capacity.
3.  **Host Performance Analysis** -- explores host portfolio size,
    response behaviour, verification, acceptance indicators, and
    Superhost representation.
4.  **Review Activity and Listing Scores** -- examines review activity
    over time and by city, listing-level score grades, and the
    relationship between price and overall rating.

The purpose is descriptive: the report helps users explore patterns and
compare segments. It does not establish that one factor causes another.

## Dataset

The primary listing source is `Listings.csv`, containing **279,712 rows
and 33 columns**.

The listing fields cover:

-   **Listing identifiers and descriptions:** `listing_id`, `name`
-   **Host information:** `host_id`, `host_since`, `host_location`,
    `host_response_time`, `host_response_rate`, `host_acceptance_rate`,
    `host_is_superhost`, `host_total_listings_count`,
    `host_has_profile_pic`, `host_identity_verified`
-   **Location:** `neighbourhood`, `district`, `city`, `latitude`,
    `longitude`
-   **Property details:** `property_type`, `room_type`, `accommodates`,
    `bedrooms`, `amenities`
-   **Pricing and stay rules:** `price`, `minimum_nights`,
    `maximum_nights`, `instant_bookable`
-   **Guest scores:** `review_scores_rating`, `review_scores_accuracy`,
    `review_scores_cleanliness`, `review_scores_checkin`,
    `review_scores_communication`, `review_scores_location`,
    `review_scores_value`

The Power BI report also uses a separate reviews table for review-level
fields such as `review_id` and `date`. This table supports the review
activity visuals on Page 4. The PBIX model contains cleaned query tables
(including `Listings_Cleaned` and `Reviews_Cleaned`).

## Tools Used

-   **Microsoft Power BI Desktop** -- data modelling, DAX calculations,
    interactive visuals, slicers, and report layout.
-   **Power Query** -- importing, cleaning, transforming, and preparing
    data.
-   **DAX** -- measures and calculated fields for KPIs and chart
    calculations.
-   **CSV / tabular source data** -- source data for the listing
    analysis.
-   **Excel** -- useful for inspecting source data and preparing or
    validating lookup information before loading it into Power BI.

## Setup Instructions

### Open the existing report

1.  Download or save `AnalystLab AirBnB Datasets.pbix`.
2.  Install and open **Power BI Desktop**.
3.  Open the PBIX file.
4.  If Power BI displays a data-source or credential prompt, follow the
    prompt and confirm the source connection.
5.  Select **Refresh** if you need to reload the data.
6.  Use the page navigation buttons and slicers to explore the report.

### Reconnect or refresh the source data

If the original source files have been moved or the report is opened on
another computer:

1.  In Power BI Desktop, select **Transform data** to open Power Query.
2.  Review the **Source** step for the listing and review queries.
3.  Update each source path to the location of the corresponding source
    file.
4.  Select **Close & Apply**.
5.  Select **Refresh** and check that the visuals update correctly.

The PBIX is the report deliverable. Keep the source data files available
if you plan to refresh or rebuild the model.

## Methodology

### 1. Data preparation

-   Loaded the listing and review data into Power BI.
-   Used Power Query to prepare cleaned query tables for analysis.
-   Reviewed key fields used in the report, including identifiers,
    dates, location, prices, host indicators, and review scores.
-   Created or used country and currency fields to support geographic
    and local-currency analysis.
-   Used the city-to-country mapping represented in the report to group
    the ten city markets: Paris, New York, Sydney, Rome, Rio de Janeiro,
    Istanbul, Mexico City, Bangkok, Cape Town, and Hong Kong.
-   Retained local currencies for price analysis rather than combining
    unconverted currency amounts into one overall price average.

### 2. Data modelling and calculations

The report uses measures and aggregations such as:

-   Listing counts and distinct host counts.
-   Average listing price, interpreted within the selected
    country/currency context.
-   Average accommodation capacity and bedroom count.
-   Superhost rate, calculated as distinct Superhosts divided by
    distinct hosts.
-   Average host response and acceptance rates.
-   Average overall, cleanliness, communication, and value scores.
-   Review counts and review dates from the separate reviews table.

Distinct counts are used for entity-level metrics such as hosts and
listings where appropriate. Visuals are designed to respond to report
filters and slicers.

### 3. Visual analysis

-   **Market overview:** map, treemap, donut, and time-based charts show
    where listings are located, the types of spaces offered, and
    host/listing patterns by host registration period.
-   **Pricing and property:** bar, column, table, and scatter visuals
    compare prices across countries and local currencies, room types,
    and accommodation capacities.
-   **Host performance:** bar, column, and donut visuals explore host
    listing portfolios, response time, identity verification, and
    Superhost distribution.
-   **Reviews and listing scores:** area, map, bar, and scatter visuals
    explore review activity, city-level review volume, score grades, and
    price against overall listing rating.

### 4. Interactivity

Slicers are included to let users filter the report by relevant fields
such as city, country, room type, property type, Superhost status, and
host identity verification. The selected filters affect the visuals
according to the report's model relationships and visual interactions.

## Key Assumptions

-   Each city in the source data is assigned to the country represented
    in the report's country mapping.
-   Each country is associated with its applicable local currency.
    France and Italy use EUR; Hong Kong uses HKD.
-   Listing prices are interpreted in their local currency. A price
    amount from one currency is not directly comparable with the same
    numeric amount in another currency.
-   The country filter is used when displaying a single average-price
    KPI so that the displayed average belongs to one local
    market/currency.
-   Host-level metrics use distinct `host_id` values where the intention
    is to count hosts rather than listings.
-   `host_since` represents the date a host joined the platform. Charts
    using this field show host-registration cohorts; they should not be
    interpreted as listing publication dates.
-   Overall listing ratings and category scores are aggregate
    listing-level scores, not individual review ratings.
-   The report's review activity trends rely on the separate reviews
    table and its `date` field.

## Limitations

-   **Currency comparability:** Local-currency prices should not be
    averaged together across countries. Cross-country price comparisons
    require a documented currency-conversion method and an exchange rate
    appropriate to the analysis period. The report does not treat a
    simple mixed-currency average as meaningful.
-   **Currency mapping:** Country and currency assignments depend on the
    city-to-country mapping. Any unmapped or ambiguous locations should
    be checked before interpreting results.
-   **Historical price context:** If the source does not provide the
    date on which each listing price was observed, the report cannot
    establish historical price movement.
-   **Host registration versus listing creation:** `host_since` is a
    host registration date, not a listing creation date. It is therefore
    a proxy for host cohort analysis, not a direct measure of new
    listings by publication date.
-   **Review coverage:** Listings with missing review scores may be
    excluded from score averages or score-based visuals. The number of
    listings with a score is not the same as the number of reviews.
-   **Causation:** Relationships shown in visuals (for example, price
    versus rating, verification versus Superhost status, or portfolio
    size versus host status) are associations only and do not prove
    causation.
-   **Data quality:** Results depend on the accuracy, completeness, and
    consistency of the supplied source data and the transformations
    applied during cleaning.
-   **Market coverage:** Findings describe the cities and records
    included in this dataset; they should not be generalised to every
    Airbnb market.

## How to Use the Dashboard

1.  Start with the KPI summary page for a quick overview.
2.  Open each analytical page to explore its charts.
3.  Use the slicers to narrow the analysis to a city, country, room
    type, property type, or host category.
4.  Hover over chart elements to inspect tooltips and compare values.
5.  When reviewing prices, always check the selected country and its
    currency before interpreting the number.
6.  Treat the report as an exploratory view of the supplied data, not as
    a live view of Airbnb's current marketplace.

## Project Deliverable

-   `AnalystLab AirBnB Datasets.pbix` -- interactive Power BI report
    containing the KPI summary and four analytical dashboard pages.
-   `Listings.csv` -- primary listing dataset used for the listing,
    property, host, and listing-score analysis.
-   A separate reviews source/table is included in the PBIX model for
    review-level activity analysis.

------------------------------------------------------------------------

*Prepared as a portfolio data analytics project.*
