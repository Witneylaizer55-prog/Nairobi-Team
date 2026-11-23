Nairobi Group 

Austin Animal Center: Cat and Dog Intake and Adoption Analysis
Project overview

This project analyses animal intake and outcome records from the Austin
Animal Center to understand patterns in the shelter journey of cats and
dogs. The work focuses on intake circumstances, animal characteristics,
age, breed, adoption outcomes, and the time animals spend in the
shelter.
The goal is to turn shelter records into useful insights that can
support better adoption campaigns, foster recruitment, shelter planning,
and animal welfare decisions.
Important: The research questions and hypotheses in this README are
proposed questions to investigate. They are not findings already
established by the data.

Project objectives

Understand the number and proportion of cats and dogs entering the
shelter and receiving different outcomes.
Compare adoption outcomes for cats and dogs.
Investigate whether age at intake or age at outcome is associated
with adoption.
Measure how long animals stay in the shelter before adoption or
another outcome.
Explore intake type and intake condition to understand the
circumstances and condition in which animals arrive.
Identify cat and dog breeds with higher or lower recorded adoption
counts and adoption proportions.
Examine changes in intake and adoption activity over time.
Translate the analysis into practical recommendations for the animal
shelter.

Data sources
1. Austin Animal Center Intakes
The intake dataset records animals entering the shelter. Depending on
the available columns, relevant fields may include:
Animal ID
Animal Type
Intake Date / DateTime
Intake Type
Intake Condition
Age upon Intake
Breed
Color
Sex upon Intake
2. Austin Animal Center Outcomes
The outcome dataset records how animals leave the shelter. Depending on
the available columns, relevant fields may include:
Animal ID
Animal Type
Outcome Date / DateTime
Outcome Type
Outcome Subtype
Age upon Outcome
Breed
Color
Sex upon Outcome
3. Dog API breed information (supplementary)
A dog breed API may be used as an additional reference for dog breed
information, such as breed names, typical life expectancy, weight
ranges, and hypoallergenic classification. This is supplementary
reference data; it does not replace the Austin shelter records and may
not match every breed label exactly.
Main concepts and variables

Concept Meaning Potential fields

Animal type Whether the animal is an Animal Type
cat or dog
Intake type How or under what Intake Type
circumstance the animal
entered the shelter
Intake condition The animal's recorded Intake Condition
condition when it
arrived
Age at intake The animal's recorded Age upon Intake
age when it entered the
shelter
Age at outcome The animal's recorded Age upon Outcome
age when it left the
shelter
Breed Recorded breed or breed Breed
description
Animal identifier Identifier used to link Animal ID
records for the same
animal
Outcome type How the animal left the Outcome Type
shelter
Intake date Date the animal entered DateTime / Intake Date
the shelter
Outcome date Date the animal left DateTime / Outcome Date
the shelter
Length of stay Elapsed time between a Calculated from dates
matched intake and
Outcome
Important distinction: age and time
Age describes how old the animal was. Analyse age at intake and
age at outcome separately where possible.
Length of stay describes how long the animal remained in the
shelter. Calculate it as outcome date minus the matched intake date.
Initial research questions and hypotheses
Research question 1: Are cats or dogs more likely to be adopted?
Proposed hypothesis (H1): The proportion of recorded outcomes that
are adoptions differs between cats and dogs.
Variables: Animal Type, Outcome Type.
Analysis: For each animal type, calculate adoption outcomes
divided by all valid recorded outcomes for that animal type. Compare
the proportions and show the results in a bar chart.

Research question 2: Does age affect adoption outcomes?
Proposed hypothesis (H2): Adoption proportions vary across age
groups, and the pattern may differ between cats and dogs.
Variables: Age upon Outcome (and/or Age upon Intake), Animal
Type, Outcome Type.
Analysis: Clean age values, create age groups, and compare the
adoption proportion in each age group. Analyse cats and dogs
separately where sample sizes allow.
Suggested age groups:
Baby: under 1 year
Young: 1 to under 3 years
Adult: 3 to under 8 years
Senior: 8 years and above

Research question 3: Are there seasonal patterns in animal intake and adoption?
Proposed hypothesis (H3): Monthly intake and outcome volumes vary
throughout the year.
Variables: Intake Date, Outcome Date, Animal Type, Outcome Type.
Analysis: Extract month and year from intake and outcome dates.
Compare monthly intake counts and monthly adoption counts using
time-series charts. Consider cats and dogs separately.

Research question 4: Which animal characteristics are associated with adoption?
Proposed hypothesis (H4): Adoption proportions differ across breed,
sex, and colour categories.
Variables: Breed, Color, Sex upon Outcome (or Sex upon Intake if
appropriate), Animal Type, Outcome Type. Age and time period may be
included as additional factors.
Analysis: Compare adoption counts and proportions across
categories. Analyse cat and dog breeds separately. Combine rare
categories carefully or report small sample sizes to avoid
misleading conclusions.

Research question 5: How long do animals stay in the shelter before adoption?
Proposed hypothesis (H5): Length of stay differs by animal type and
may also vary by age group, breed, intake type, and intake condition.
Variables: Animal ID, Intake Date, Outcome Date, Animal Type,
Age upon Intake, Breed, Intake Type, Intake Condition, Outcome Type.
Analysis: Match each adoption outcome to the most recent valid
preceding intake for the same Animal ID. Calculate length of stay in
days. Compare median and distribution of stay days for cats and dogs
and across relevant groups.

Research question 6: Does intake type or intake condition relate to adoption outcomes?
Proposed hypothesis (H6): Adoption proportions vary according to the
recorded intake type and intake condition.
Variables: Intake Type, Intake Condition, Animal Type, Outcome
Type, Animal ID.
Analysis: Link intake and outcome records using Animal ID and
dates. Compare subsequent outcomes across intake types and
conditions. Make clear how unmatched or repeated records are
handled.

Research question 7: Which cat and dog breeds have the highest recorded adoption activity?
Proposed hypothesis (H7): Recorded adoption counts and adoption
proportions differ between breeds.
Variables: Breed, Animal Type, Outcome Type, Animal ID.
Analysis: Rank cat breeds and dog breeds separately by adoption
count. Also calculate adoption proportions using all valid outcomes
within each breed. Show the number of records for each breed so that
small groups are not overinterpreted.

Key metrics and definitions

Adoption proportion among recorded outcomes
For a given animal group:
Adoption proportion = Number of adoption outcomes / Number of valid recorded outcomes
Multiply by 100 to express the result as a percentage.
This metric describes the share of recorded outcomes that are adoptions.
It is not automatically the probability that an animal entering the
shelter will be adopted, because the intake and outcome records may
cover different time windows and some animals may not yet have an
outcome.
Intake and outcome counts
Monthly intake count: Number of intake records in each month.
Monthly adoption count: Number of adoption outcome records in
each month.
These are event counts. An animal may have more than one intake or
outcome record over time.
Length of stay
Length of stay (days) = Outcome date - Matched intake date
Use the most recent valid intake before the outcome for the same Animal
ID. Review duplicate, repeated, missing, or inconsistent records before
calculating summary statistics. A zero-day stay may be valid but should
be checked.
Breed adoption count versus breed adoption proportion
Adoption count: Number of adoption outcome records for a breed.
Adoption proportion: Adoption outcomes divided by all valid
outcomes for that breed.
A breed with the highest adoption count may simply have more records.
Reporting both measures gives a fairer comparison.
Data cleaning and preparation plan
Load the intake and outcome CSV files with Pandas.
Inspect dataset dimensions, column names, data types, missing
values, and duplicate records.
Standardise column names (lowercase, underscores, consistent
spelling).
Trim unnecessary whitespace in text columns and standardise category
labels.
Parse intake and outcome dates consistently; retain or document
original date values where useful.
Clean age fields while preserving the original age text. Convert
recognised years, months, weeks, and days into a numeric age
measure. Keep unknown or unparseable ages missing rather than
converting them to zero.
Create age groups using documented boundaries.
Standardise animal type labels so cats and dogs can be compared
consistently.
Check Animal ID values and investigate missing identifiers.
Remove exact duplicate rows where appropriate, while retaining an
audit of removed or flagged records.
Link intake and outcome records by Animal ID and chronology. Do not
join on Animal ID alone if this creates incorrect many-to-many
matches.
Calculate length of stay only for defensible intake-outcome matches.
Review unusual records, such as negative durations, repeated intake
matches, zero-day stays, and very long stays.
Export cleaned datasets and analysis-ready tables separately from
the raw files.
Suggested analysis and visualisations

Analysis Suggested visualisation

Adoption proportion: cats vs dogs Bar chart
Adoption by age group Grouped bar chart
Monthly intakes and adoptions Line chart
Breed adoption counts Horizontal bar chart
Breed adoption proportions Horizontal bar chart with sample
counts
Length of stay by animal type Box plot or histogram
Length of stay by age group Box plot
Outcomes by intake type or Stacked bar chart or proportion
condition chart
Use clear titles, axis labels, sample sizes, and percentage formatting.
Avoid interpreting a category with very few records as a reliable trend.
Statistical testing
Where appropriate, use a chi-square test of independence to investigate
associations between categorical variables, such as Animal Type and
Outcome Type, or Age Group and Outcome Type.
Null hypothesis (H0): There is no association between the two
categorical variables.
Alternative hypothesis (H1): There is an association between the
two categorical variables.
Check expected cell counts before relying on the chi-square
approximation. If counts are sparse, combine categories only when
substantively justified or use an appropriate exact test. Statistical
association does not prove causation.
For comparisons of length of stay, inspect distributions and outliers.
The data may be skewed, so report medians and interquartile ranges as
well as means. Select statistical tests based on the data and
assumptions.
Business opportunities
The analysis may help the Austin Animal Center to:
Direct adoption promotion toward animal groups with lower adoption
proportions.
Design age-specific campaigns for puppies, kittens, adult animals,
and senior animals.
Plan staffing and foster capacity around seasonal intake patterns.
Improve animal profiles and promotion using breed and animal
characteristics.
Identify groups with longer shelter stays and consider additional
support.
Better understand the relationship between intake circumstances,
animal condition, and later outcomes.
Recommendations must be based on the results of the analysis, not on the
proposed hypotheses alone.
Project limitations and considerations
The records describe a particular shelter and should not
automatically be generalised to all shelters.
Intake and outcome datasets may have different date coverage or
incomplete records.
An animal can have multiple shelter visits, so record-level counts
are not necessarily counts of unique animals.
Some animals may have no recorded outcome during the dataset period.
Age values may be approximate or inconsistently recorded.
Breed and colour fields may contain mixed, unknown, or multiple
labels.
A high adoption count does not necessarily mean a high adoption
proportion.
The Dog API may use breed names that do not align exactly with
shelter breed descriptions.
Observational data can show associations but cannot by itself
establish that a characteristic causes adoption.
Suggested project workflow
Data collection and source assessment.
Data understanding and initial exploration.
Data cleaning and quality checks.
Data structuring and intake-outcome matching.
Exploratory data analysis.
Research question analysis and hypothesis testing.
Visualisation and interpretation.
Business recommendations.
Final report and presentation.
Tools and technologies
Python
Pandas
NumPy
Matplotlib
Seaborn
Jupyter Notebook
Austin Animal Center open data
Dog API (supplementary breed reference)
Expected deliverables
Reproducible Jupyter Notebook(s) documenting data cleaning,
structuring, and analysis.
Cleaned intake and outcome datasets.
An analysis-ready adoption dataset with documented matching rules.
Summary tables and visualisations addressing the research questions.
A final report with evidence-based conclusions and business
recommendations.
