# Medical Appointment No-Show Analysis

Which patients are most likely to miss their appointments - an analysis of 110,521 medical appointments.

---

## The Question

Which patients are most likely to miss their medical appointments and does an SMS reminder reduce no-shows?

This matters because missed appointments waste clinical time, lengthen waiting lists, and worsen patient outcomes. If clinics can identify who's likely to no-show, they can intervene before it happens.

---

## The Data

Source: Medical Appointment No-Shows (Kaggle, Brazil, 2016).

· 110,521 appointments after cleaning

· 15 columns covering patient demographics, scheduling and appointment dates, chronic conditions, SMS reminder status, and no-show outcome

· Each row is one appointment, a patient may appear multiple times

---

## Method

1.  Before building anything I first checked:

· How many rows and columns?

· What are the column types?

· What are the values in the outcome column (NoShow)?

· Which columns are missing or mostly empty?

· Which columns are likely to matter?

2. Cleaning in Power Query:

· Converted ScheduledDay and AppointmentDay to Date type

· Created a LeadTime column (days between booking and appointment)

· Filtered out rows with negative lead times (data errors)

· Created a NoShowFlag column (1 for no-show, 0 for showed up) this is required for aggregating the outcome as a rate


3. Analysis:

· Built PivotTables for each candidate variable against NoShowFlag

· Used Average of the flag column to calculate the no-show rate per group (avoids the double-series chart problem)

· Ranked findings by strength of pattern

---

## Headline Insight

Appointment lead time is the strongest predictor of no-show.

Patients who booked their appointment 10+ days in advance no-showed at 32.51%. Those who booked within 0-9 days no-showed at 14.29%.

Risk jumps sharply at 10 days, then plateaus around 30-35% for all longer lead times.

That's a 2.3× difference
The single biggest driver in the dataset.

---

## Supporting Findings

1. Age : The 10-19 age band had the highest no-show rate (25.17%). Rates decline with age, bottoming at 60-79 (~15%), then rise slightly at 80+.

2. SMS reminders (counterintuitive result) : Patients who received an SMS had a higher no-show rate (27.57%) than those who didn't (16.70%). This is likely selection bias, clinics probably target reminders at patients they consider high-risk. The data cannot tell us whether reminders help or hurt.

3. Scholarship enrolment : Small effect. Patients on welfare support no-showed at 23.74% vs 19.80% for those without.

4. Gender : No effect. Male 19.96%, Female 20.31%.

---

## Recommendation

Hospitals and clinics should:

1. Prioritise short lead times. Book appointments within 0-9 days where clinically possible.
2. Target the 10-29 age group with extra reminders or follow-up calls.
3. Test SMS reminders with random assignment to measure real impact, the current data can't tell us.
4. Monitor no-show rates monthly. It is an operational metric worth tracking.

---

## Limitations

· Old data : from 2016, patterns may have shifted.

· Dataset was from a single country : Brazil only. May not generalise to other regions.

· SMS cannot be causally interpreted : no random assignment, so the reminder's true effect is unknown

· Small groups in the tail : lead times beyond ~70 days have too few appointments to be reliable. Analysis focuses on the well-populated range.

---

## Tools

· Excel (Power Query, PivotTables, PivotCharts, slicers, KPI formulas).

---

## Files

- `README.md` - this document
- `dashboard.png` - interactive dashboard screenshot
- `no-show-analysis.xlsx` - full Excel workbook (Power Query steps, pivots, PivotCharts, dashboard)

*Note: the workbook contains an interactive slicer that filters all four charts.*
