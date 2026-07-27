# Disclosure thresholds and the exit margin

**Do firms use the escape hatch in US emissions-disclosure law?**

The Greenhouse Gas Reporting Program (40 CFR Part 98) requires facilities emitting
≥25,000 tCO₂e per year to report, and EPA publishes the reports facility by facility.
Less well known is **40 CFR 98.2(i)**, which lets a facility already in the program stop
reporting after *five consecutive years below 25,000* or *three consecutive years below
15,000* — and requires it to resume if emissions ever reach 25,000 again.

That provision turns a static threshold into a dynamic rule with two waiting periods, and it
makes the avoidance decision a dated, observable event rather than a shape in a histogram.

**[→ Read the findings](https://lyl1710640659-del.github.io/Capstone---EPA-and-GHGRP/)** &nbsp;·&nbsp;
**[→ See the analysis](01_descriptive_sweep.ipynb)**

---

## Headline results

Full public GHGRP panel: **94,378 facility-years, 8,778 facilities, 2010–2023.**

**No bunching at either threshold.** The density is smooth through 15,000, and the
discontinuity at 25,000 is mechanical — facilities below the threshold do not report at all,
so the sample is truncated exactly at the cutoff. Firms are not manipulating reported
emissions levels to escape disclosure.

**But exit responds sharply.** Facility-years eligible to leave under 98.2(i) end in exit
**21.0%** of the time; ineligible ones, **1.5%**. That is 996 exits out of 4,755 eligible
facility-years.

**Excess mass at exactly the statutory waiting periods.** Counting the consecutive years a
facility spent below each threshold immediately before leaving:

| Sample | Threshold | Statutory wait | Excess @ 3 yrs | Excess @ 5 yrs |
|---|---|---|---|---|
| All threshold-bound | 15,000 | 3 years | **+199%** | −56% |
| All threshold-bound | 25,000 | 5 years | +63% | **+163%** |
| All threshold-bound | 40,000 | *placebo* | +14% | −7% |
| All threshold-bound | 100,000 | *placebo* | −32% | −14% |
| Ex oil & gas, ex-2015 | 15,000 | 3 years | **+178%** | −43% |
| Ex oil & gas, ex-2015 | 25,000 | 5 years | +38% | **+195%** |
| Ex oil & gas, ex-2015 | 40,000 | *placebo* | +28% | −20% |

Every real waiting period is significant at 95% (bootstrap, 2,000 reps); every placebo
threshold straddles zero. The result survives dropping oil, gas, pipelines, refining and
utilities entirely, along with the whole 2014–16 oil-price-collapse exit wave.

> **Firms are not managing their emissions around the threshold. They are managing when they
> leave.**

---

## What is here

| File | |
|---|---|
| `01_descriptive_sweep.ipynb` | Full descriptive analysis, 2010–2023. Runs end to end on the public download. |
| `ghgrp_load.py` | Panel loader — stacks EPA's annual facility files and derives the 98.2(i) eligibility variables. |
| `docs/index.html` | Write-up of the findings, with figures. |
| `output/` | Figures and tables produced by the notebook. |

## Reproducing

```bash
pip install pandas numpy matplotlib openpyxl statsmodels
```

Download the EPA annual files — free, no registration — from
[EPA GHGRP Data Sets](https://www.epa.gov/ghgreporting/data-sets) (the *Data Summary
Spreadsheets* archive), and place `ghgp_data_2010.xlsx` … `ghgp_data_2023.xlsx` in `data/`.
Then run the notebook.

The per-year files are used rather than the multi-year summary workbook, which starts in 2011,
stamps only the *latest* reported subpart on every year, and omits the
continuous-emissions-monitoring flag.

## Caveats

- **"Exit" is inferred from disappearance from the panel.** EPA collects an actual
  Notification to Discontinue Reporting; the two should be reconciled.
- **Stopping reporting is not the same as shutting down.** Distinguishing the two requires
  facility-level survival data, which is not in this repository. This is the largest open gap.
- The always-covered comparison group (electricity, aluminum, ammonia, cement, landfills) is
  **not** a clean placebo for the waiting-period test — it shows elevated mass at 3 and 5 years
  for every threshold including the placebos, an artefact of shorter panels and smaller n. The
  placebo used here is a different threshold within the same facilities.
- Subpart letters defining that group should be verified against 40 CFR 98 Table A-3.

## References

- Tomar, S. (2023). Greenhouse Gas Disclosure and Emissions Benchmarking.
  *Journal of Accounting Research* 61(2), 451–492.
- Kleven, H. (2016). Bunching. *Annual Review of Economics* 8, 435–464.
- [40 CFR 98.2](https://www.ecfr.gov/current/title-40/chapter-I/subchapter-C/part-98/subpart-A/section-98.2)

---

Yiling Long · July 2026
