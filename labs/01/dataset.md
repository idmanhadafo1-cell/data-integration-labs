# Dataset candidate: Wikipedia page views (Wikimedia Pageviews)

**Team question:** How are public search interest and media attention related to the development of concert ticket prices in Germany?
**My part:** public search interest, measured as monthly page views of Wikipedia articles.
**Articles:** *Taylor Swift* and *Oasis* on de.wikipedia.org – two artists with big public debates about ticket prices: the Eras Tour in Germany (July 2024) and dynamic pricing for the Oasis reunion (August 2024).
**Checked on:** 3 November 2026

## Contents

- [Task 5 · Find a dataset](#task-5--find-a-dataset)
- [Task 6 · Profile the dataset](#task-6--profile-the-dataset)
- [Task 7 · Review it with the FAIR principles](#task-7--review-it-with-the-fair-principles)
- [Task 8 · Plan what to combine it with](#task-8--plan-what-to-combine-it-with)
- [Sources](#sources)

---

## Task 5 · Find a dataset

### 1. Where I searched

| Kind of source | Source | Search terms | Result |
|----------------|--------|--------------|--------|
| State portal | [Open.NRW](https://open.nrw/) | konzert | 8 hits – statistics on concert orchestras and visits in NRW, but no data on public interest in artists |
| National / international portal | [Destatis GENESIS](https://genesis.destatis.de/), [Eurostat](https://ec.europa.eu/eurostat) | Verbraucherpreisindex, Konzert, HICP | Monthly price indices for cinemas, theatres and concerts – prices, but no data on attention |
| Search engine / repository | Google Dataset Search, [Wikimedia Analytics API](https://doc.wikimedia.org/analytics-api) | pageviews, Wikipedia page views | **Wikimedia Pageviews**: page views per article, per day or month, since July 2015, open licence |
| Other | [Google Trends](https://trends.google.de) | Taylor Swift, Oasis | Relative search interest (0–100) – useful, but no open licence, so not my main dataset |

Social media data (Instagram, TikTok, X) is mostly not openly available. Wikipedia page views are an open substitute for "public interest".

### 2. Search like a machine

Request to the Open.NRW API:

```
https://open.nrw/api/3/action/package_search?q=konzert&rows=1
```

- **Hits (`count`):** 8
- **Title of the first hit:** *Selbstständige Konzertorchester, Mitglieder, Konzerte und Besuche – Land – Spielzeit* (Landesdatenbank NRW)
- **Where the licence is given:** both for the whole dataset (`license_id`) and for each file (`license` under `resources`): `dl-by-de/2.0`, Datenlizenz Deutschland – Namensnennung 2.0.
- **Do not trust every field:** the same record says `"isopen": false` and `"non_open": "true"`, although dl-by-de/2.0 is an open licence.

The state portal has nothing on public interest in concerts – that is why my dataset comes from Wikimedia.

### 3. My dataset

**Wikimedia Pageviews – monthly page views of *Taylor Swift* and *Oasis* on de.wikipedia.org, January 2017 – December 2025.**
Requested as JSON directly from the original publisher, the Wikimedia Foundation, and saved as one CSV file:

```
https://wikimedia.org/api/rest_v1/metrics/pageviews/per-article/de.wikipedia/all-access/user/Taylor_Swift/monthly/2017010100/2025123100
https://wikimedia.org/api/rest_v1/metrics/pageviews/per-article/de.wikipedia/all-access/user/Oasis/monthly/2017010100/2025123100
```

---

## Task 6 · Profile the dataset

### 1. Facts

| | Wikimedia Pageviews – *Taylor Swift*, *Oasis*, de.wikipedia |
|---|---|
| Publisher | Wikimedia Foundation, [Analytics API](https://doc.wikimedia.org/analytics-api) |
| Link | [Taylor Swift](https://wikimedia.org/api/rest_v1/metrics/pageviews/per-article/de.wikipedia/all-access/user/Taylor_Swift/monthly/2017010100/2025123100), [Oasis](https://wikimedia.org/api/rest_v1/metrics/pageviews/per-article/de.wikipedia/all-access/user/Oasis/monthly/2017010100/2025123100) (API); [Pageviews tool](https://pageviews.wmcloud.org) for charts |
| Formats | CSV (tool), JSON (API), compressed text files ([dumps](https://dumps.wikimedia.org/other/pageviews/)) |
| Size | API: 108 items per article with 7 fields each. My CSV: 1 file, 108 rows (months), 3 columns (`month`, `Taylor_Swift`, `Oasis`) |
| Coverage | German Wikipedia, January 2017 – December 2025, monthly totals per article. Available since July 2015, per day or month, for every article and language |
| Last update and frequency | Updated daily; monthly values appear after the month ends |
| Licence | [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/): "Data provided by the API is available under the CC0 1.0 license" ([access policy](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/documentation/access-policy.html)) |

### 2. Stars

**★★★ – three stars:** openly licensed (CC0), structured, in an open format (CSV / JSON).
**Missing for the fourth star:** Articles are identified by their title (`Taylor_Swift`), not by a stable URI. If each row linked to the Wikidata item of the artist (e.g. Taylor Swift = Q26876), others could connect the data to concerts, albums or other languages.

### 3. Open the data

**Tools:** Chrome to open the JSON from the API; a short Python script (with Claude's help, see `AI_USAGE.md`) to turn it into a CSV and calculate the statistics.

| Column | Minimum | Maximum | Mean |
|--------|--------:|--------:|-----:|
| Taylor Swift | 18,858 (September 2018) | 518,532 (July 2024) | 65,739.8 |
| Oasis | 7,499 (September 2023) | 169,963 (August 2024) | 14,784.0 |

**Empty cells:** 0 in the column *Oasis* – all 108 months are there. The API would leave out a missing month instead of writing an empty value, so I counted the rows.

**Odd things:**

- **Wrong article title gives no error:** `Oasis_(Band)` – the title I guessed – returned two months with `"views": 0` instead of an error. `Oasis_(britische_Band)` returned 404. The German article is simply called *Oasis*. Without checking, I would have used zeros as data.
- **Dates:** the API uses timestamps like `2024080100` (year, month, day, hour), not ISO 8601 `2024-08`. I converted them in my CSV.
- **Peaks match concert news:** Taylor Swift peaks in July 2024, when the Eras Tour played in Gelsenkirchen, Hamburg and Munich. Oasis jumps from 8,314 (July 2024) to 169,963 (August 2024) – the month of the reunion announcement and the debate about dynamic pricing – and again in July 2025, when the tour started. Useful for H5.
- **Only one language:** de.wikipedia is read in Germany, Austria and Switzerland – not only in Germany.
- **Bots:** I chose `agent=user`. Without it, automated traffic is counted too and the numbers are higher.
- **Redirects and languages:** views of redirect titles and of other language editions are counted separately.
- **Encoding / separators:** JSON in UTF-8, no problems. In URLs, special characters must be encoded, e.g. brackets or umlauts.

### 4. Data dictionary

The API returns these fields for every month (the CSV from the tool has one column per article):

| Field | Meaning | Type and unit | Example |
|-------|---------|---------------|---------|
| `project` | Wikipedia language edition | Text | `de.wikipedia` |
| `article` | Title of the article | Text, underscores instead of spaces | `Taylor_Swift` |
| `timestamp` | Start of the month | Text, `YYYYMMDDHH` | `2024070100` |
| `agent` | Type of reader | Text: `user`, `spider`, `automated` | `user` |
| `views` | Page views in that month | Integer, views per month | `518532` |

**Does the publisher document the fields?** Yes – in the [Analytics API documentation](https://doc.wikimedia.org/analytics-api) and on [Wikitech](https://wikitech.wikimedia.org/wiki/Data_Platform/Data_Lake/Traffic/Pageviews), including the definition of a page view.

### 5. Licence

- **Open?** Yes. CC0 is a public domain dedication and [conforms to the Open Definition](https://opendefinition.org/licenses/).
- **When I reuse it:** no conditions. We credit the source anyway so the project is traceable. The API asks clients to send a *User-Agent* that identifies the app – a rule for access, not for reuse.
- **Attribution line (TASL):**
  > "Pageviews of the articles Taylor Swift and Oasis, de.wikipedia, 2017–2025" by Wikimedia Foundation, [doc.wikimedia.org/analytics-api](https://doc.wikimedia.org/analytics-api), [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)

### 6. People

No personal data about readers: the API only gives totals per article and month – no IP addresses, user names or single visits. The articles are about public figures (artists), which is not a privacy problem for counting views.

---

## Task 7 · Review it with the FAIR principles

| Principle | Rating | Evidence |
|-----------|:------:|----------|
| **F1** Unique, persistent identifier | ~ | The API URL is stable and contains project, article and period, but there is no DOI |
| **F2** Rich metadata | ✓ | Every row states project, article, granularity, access type and agent |
| **F3** Metadata include the identifier | ✓ | The request URL itself identifies the data |
| **F4** Registered in a searchable resource | ~ | Documented by Wikimedia, but not listed on GovData, Open.NRW or data.europa.eu |
| **A1** Retrievable with a standard protocol | ✓ | HTTPS REST API, no login, no key |
| **A2** Metadata remain if the data is gone | ~ | Not stated; the dumps since 2015 are archived on [dumps.wikimedia.org](https://dumps.wikimedia.org/other/pageviews/) |
| **I1** Formal, shared language | ✓ | JSON and CSV in UTF-8 |
| **I2** FAIR vocabularies | ~ | Fixed values like `monthly`, `user`, but timestamps are not ISO 8601 |
| **I3** References to other data | ✗ | No link to Wikidata or other datasets |
| **R1** Rich description of attributes | ✓ | API documentation and page view definition on Wikitech |
| **R1.1** Clear licence | ✓ | "Data provided by the API is available under the CC0 1.0 license" ([access policy](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/documentation/access-policy.html)) |
| **R1.2** Provenance | ✓ | Definition of a page view and filtering of bots are documented |
| **R1.3** Community standards | ~ | REST and JSON, but no DCAT metadata |

**Summary:** very accessible and clearly licensed. Weakest point: interoperability – no links to other data and no ISO dates.

---

## Task 8 · Plan what to combine it with

_Planned together with the team – follows after our meeting._

---

## Sources

- "Pageviews of the articles Taylor Swift and Oasis, de.wikipedia" by Wikimedia Foundation, [Analytics API](https://doc.wikimedia.org/analytics-api), [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)
- Licence statement: [Wikimedia Analytics API access policy](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/documentation/access-policy.html)
- Page view definition: [Wikitech](https://wikitech.wikimedia.org/wiki/Data_Platform/Data_Lake/Traffic/Pageviews)
- Metadata search: [Open.NRW CKAN API](https://open.nrw/api/3/action/package_search?q=konzert&rows=1)
