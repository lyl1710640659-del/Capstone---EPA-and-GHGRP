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
- **Stopping reporting is not the same as shutting down.** Separating the two requires
  establishment-level survival data — plant operating status, employment — which this public
  release does not contain. This is the largest open gap.
- The always-covered comparison group (electricity, aluminum, ammonia, cement, landfills) is
  **not** a clean placebo for the waiting-period test — it shows elevated mass at 3 and 5 years
  for every threshold including the placebos, an artefact of shorter panels and smaller n. The
  placebo used here is a different threshold within the same facilities.
- Subpart letters defining that group should be verified against 40 CFR 98 Table A-3.
- Tomar (2023) finds GHGRP disclosure induced real emissions reductions through peer
  benchmarking. That channel pushes facilities toward the threshold for reasons unrelated to
  avoidance, and the two have not yet been separated.

---

## Status and next steps

**Work in progress.** What is here is the descriptive stage — establishing what the data can
and cannot support before committing to a design. Three of the planned steps, in order of
priority:

**1 · Validate the exit measure.** Reconcile panel disappearance against EPA's Notification to
Discontinue Reporting filings, so that "exit" is an observed regulatory act rather than an
inference.

**2 · Separate exit from shutdown.** Link facilities to establishment-level operating and
employment records (NETS, QCEW) to confirm that facilities leaving the program are still
running. Without this the central claim — that firms *choose* to stop disclosing — cannot be
distinguished from ordinary plant closure. This is the binding constraint on the project.

**3 · Price the behaviour.** Excess mass in a static density maps to a structural cost through
the standard bunching machinery (Kleven 2016). Here the notch is in *waiting time* rather than
in the density, and whether the same logic transfers is unresolved. Until it is, the result is
a duration, not a price.

Two further directions, contingent on the above:

- **A policy layer.** Whether exit accelerates after deregulatory shocks — the June 2017 Paris
  withdrawal announcement in particular — with 98.2(i) eligibility as the exposure margin. The
  complication is that the 2014–16 oil collapse sits immediately before, and the Clean Power
  Plan regulated precisely the always-covered comparison group.
- **A second setting.** Whether TRI or the National Emissions Inventory contain comparable
  cessation provisions. If so, this becomes a study of disclosure thresholds in general rather
  than of one EPA rule.

## References

- Tomar, S. (2023). Greenhouse Gas Disclosure and Emissions Benchmarking.
  *Journal of Accounting Research* 61(2), 451–492.
- Kleven, H. (2016). Bunching. *Annual Review of Economics* 8, 435–464.
- Kleven, H. & M. Waseem (2013). Using Notches to Uncover Optimization Frictions and Structural
  Elasticities. *Quarterly Journal of Economics* 128(2), 669–723.
- [40 CFR 98.2](https://www.ecfr.gov/current/title-40/chapter-I/subchapter-C/part-98/subpart-A/section-98.2)

---

Elaine · July 2026 · comments welcome via
[Issues](https://github.com/lyl1710640659-del/Capstone---EPA-and-GHGRP/issues)
