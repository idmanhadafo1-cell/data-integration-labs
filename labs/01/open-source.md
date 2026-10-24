# Look inside an open source project: pandas

**Project:** [pandas-dev/pandas](https://github.com/pandas-dev/pandas) – a Python library for working with tables of data.
**Checked on:** 24 October 2026

## 1. Licence

pandas uses the **BSD 3-Clause** licence ([LICENSE](https://github.com/pandas-dev/pandas/blob/main/LICENSE)).
It is **permissive**, not copyleft: I may use, change and share the code, also in closed-source projects.
If I copy pandas code into my own project, I must keep the copyright notice and the licence text, and I must not use the pandas name or its contributors' names to promote my project.

## 2. What machines see

| Repository | `license.spdx_id` | Meaning |
|------------|-------------------|---------|
| [pandas-dev/pandas](https://api.github.com/repos/pandas-dev/pandas) | `BSD-3-Clause` | GitHub found the licence file and recognised it as BSD 3-Clause. |
| [my lab repository](https://api.github.com/repos/idmanhadafo1-cell/data-integration-labs) | `MIT` | GitHub recognised the MIT licence I added from the template. |
| [owid/co2-data](https://api.github.com/repos/owid/co2-data) | `null` | There is no licence file GitHub can read; the licence (CC BY 4.0) is only written in the [README](https://github.com/owid/co2-data#license), so machines cannot find it. |

## 3. Community files

Found under [Insights → Community standards](https://github.com/pandas-dev/pandas/community):

| File | Present? |
|------|----------|
| README | ✅ |
| LICENSE | ✅ |
| CONTRIBUTING | ✅ (in the [pandas docs](https://pandas.pydata.org/docs/development/contributing.html)) |
| CODE_OF_CONDUCT | ✅ (in the shared [pandas-dev/.github](https://github.com/pandas-dev/.github) repository) |

## 4. People

- **Contributors:** 3,876 (sidebar of the [repository](https://github.com/pandas-dev/pandas))
- **Who decides:** The **Core Team** decides by consensus and reviews and merges pull requests. Wes McKinney, who created pandas, is the "Benevolent Dictator for Life" and has the final say, but rarely uses it. ([Governance](https://pandas.pydata.org/about/governance.html))

## 5. Money

pandas is mostly built by volunteers and by developers paid by companies.

- **NumFOCUS**, a non-profit foundation, is the fiscal sponsor and manages donations.
- **Companies:** Nvidia employs a contributor; Bodo supports development financially; pandas is part of the Tidelift subscription.
- The README shows a "Powered by NumFOCUS" badge, and the repository has a *Sponsor this project* section.

Sources: [Sponsors](https://pandas.pydata.org/about/sponsors.html), [Governance](https://pandas.pydata.org/about/governance.html)

## 6. Activity

- **Latest release:** [pandas 3.0.6](https://github.com/pandas-dev/pandas/releases), 17 September 2026
- **Open issues:** about 1,800 ([Issues](https://github.com/pandas-dev/pandas/issues))
- **Open pull requests:** 295 ([Pull requests](https://github.com/pandas-dev/pandas/pulls))

## 7. Your way in

According to the [contributing guide](https://pandas.pydata.org/docs/development/contributing.html):

1. Find an issue and comment `/take` so a bot assigns it to you.
2. Fork the repository and create a new branch.
3. Make the change and add tests.
4. Open a pull request that links to the issue (e.g. `closes #1234`).
5. Keep the automatic tests green, react to reviews; a maintainer then merges it.

**Newcomer labels:** No. pandas does not use a *good first issue* label – GitHub reports it as an invalid label when I [filter the issues](https://github.com/pandas-dev/pandas/issues?q=is:issue%20is:open%20label:%22good%20first%20issue%22). Instead, the contributing guide links to the blog post [Don't start with good first issues](https://labs.quansight.org/blog/dont-start-with-good-first-issues) and warns against issues labelled *Needs Triage*, *Needs Discussion* or *Needs Info*. GitHub itself suggests some issues for newcomers on the [contribute page](https://github.com/pandas-dev/pandas/contribute).
