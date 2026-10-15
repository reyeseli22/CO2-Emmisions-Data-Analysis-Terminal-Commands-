# Data Literacy Field Notes & Terminal Log

**The scenario:** A climate-and-energy nonprofit wants to use this
country-level energy and emissions dataset to help decide where to direct
community-protection and climate-support efforts — but the file just
landed with zero documentation. Before anyone can trust a decision built
on top of it, you need to figure out what's actually in it — what each
column really holds, and anything that looks off. That's what this whole
file walks through: the real, everyday first pass any analyst runs on an
unfamiliar file, and the real answers you need before this data is safe
to act on.

Dataset: `../data/co2_emissions_2022.csv` (see `../data/SOURCE.md`). Each
section below describes what you're trying to find out — **figuring out
which command (and which flags) actually gets you there is part of what
this project tests**, so the exact command isn't given. Where a command
belongs, you'll see a `# TODO:` comment describing the goal instead of a
ready-to-run command; replace the comment with the real command you used.
Paste the **real output** you got underneath, then write your answer based
on what you actually saw, not what you'd expect. Work through this in
order; open the raw file before anything else.

Run all commands from the repo root — the top-level folder you land in
after cloning *your own* copy of this repo (`git clone ...` then `cd
your-repo-name`, see `README.md` Step 3; not this template) — or `cd` into
`data/` first and drop the `data/` prefix — your choice, just be
consistent.

**This one file is your whole record** — the commands you ran, their real
output, and your written answers, all together in the order you actually
did the work. There's no separate log file to keep in sync with this one;
whenever you write a command down anywhere in this file, use a fenced code
block tagged `bash`, like this:

````
```bash
git status
```
````

Three backticks, the word `bash`, your command, three backticks to close —
it renders with syntax highlighting and makes the command copy-pasteable.

## Setup log

Before jumping into the dataset, log the commands you actually ran to set
this repo up (see `README.md`) — `git init`/clone, creating your
`.gitignore`, your first commit. Add to this as you go, don't
reconstruct it from memory at the end.

```bash
git clone "https"
cd <repo>
touch .gitignore
```

## 1. First look at the raw file

Before trusting anything about this file's structure, you want a quick,
safe peek at it — not the whole 254-row file, just the **first 5 lines**,
enough to see the shape of it without scrolling past everything.

```bash
cd data 
head -n 5 co2_emissions_2022.csv
```

**Output:**
country,iso_code,year,population,gdp,co2
Afghanistan,AFG,2022,40578847,53303471617,10.170
Africa,,2022,1445862695,,1459.114
Africa (GCP),,2022,,,1459.103
Albania,ALB,2022,2827614,36171005594,4.498

**What I notice:** There are 6 data types, the data is unstructured, separated by commas,Africa, Afghanistan, Albania, are 3 countries included although africa is not a country. Africa is listed twice and one entry is missing a value in the second column (iso)

## 2. Column names

Next you want to see just the column names by themselves — one per line is
a lot easier to scan than one long comma-separated row.

```bash
head -n 1 co2_emissions
```


**Output:**
country,iso_code,year,population,gdp,co2

## 3. Column-by-column data type table

For each column, you want to preview real values — **the first 6 values**
of just that one column — without scrolling through every field on every
row. Column numbers for reference: `country`=1, `iso_code`=2, `year`=3,
`population`=4, `gdp`=5, `co2`=6.

```bash
awk -F',' '{print $1,$2,$3,$4,$5,$6}' co2_emissions_2022.csv | head -n 7
```

Fill in the table from what you actually saw — not a guess from the column
name alone:

| Column | Inferred type | How I can tell |
|country|str|text|
| iso_code | str | text, represents countries |
| year | date| designates a specific time|
| population | int| numbers representing numbers, no decimals |
| gdp| int| Numbers are present, no decimals|
| co2 | float | contains a "floating" decimal |

**In your own words:** A list/array is one group of values with no particular organization. A table separates values in to various lines and columns in a consistent formatwhat's the actual difference between a list/array
and a table? (Not a definition you looked up — explain it the way you'd
explain it to a friend who's never coded. No command needed for this one,
just think about the table you just filled in above.)

A list/array is one group of values with no particular organization. A table separates values in to various lines and columns in a consistent format

## 4. Structured or unstructured?

State whether this dataset is structured or unstructured, and why.

Structured because values are separated into rows and columns. However the quality of the data is poor, causing us to question whether it is semi/unstructured

## 5. Before you trust this data

Your first look (see section 1) turned up a row with a suspiciously
**blank** `iso_code`. Before you build anything on this data, you want to
know exactly how many of the 254 rows share that blank — is it a one-off,
or a real pattern worth flagging before anyone draws conclusions from it?
You may need more than one command for this — piping (`|`) feeds one
command's output into the next as input.

```bash
cut -d',' -f2 co2_emissions_2022.csv|tail -n +2 | grep -c '^$'
```

**Output:**
36

```bash
cut -d',' -f5 co2_emissions_2022.csv|tail -n +2 | grep -c '^$'
```

**Output:**
89

List **at least 2** specific things you'd want to know about how this
dataset was collected, before trusting any conclusion drawn from it — ground
at least one in the counts you just found.

**My 2 concerns:**
1. Various instances where continents or non-countries are listed
2. Why are there so many missing values? 

## 6. Data-quality question for the source

Take the **most specific and checkable** of the two concerns above, and
phrase it as a real question you'd send to the data's source/maintainer. A
good test: could they actually answer it with a concrete yes/no or fact —
not "is this data good?"

I noticed that across 2 of 6 columns 125 values are missing and I can see more in the other column. Could this have resulted from an issue in the data collection process?

## 7. Something you're actually curious about

Different question from #6 — that one was about checking the data's
trustworthiness. This one's about you: what's something you're genuinely
curious to explore using this data? Pick two specific countries you're
curious to compare, and look up their full rows.

```bash
grep -n "albania" co2_emissions_2022.csv
grep -n "Africa" co2_emissions_2022.csv
```

**Output:**
5:Albania,ALB,2022,2827614,36171005594,4.498

3:Africa,,2022,1445862695,,1459.114
4:Africa (GCP),,2022,,,1459.103
45:Central African Republic,CAF,2022,5098038,3752056621,0.377
215:South Africa,ZAF,2022,62378417,723559323969,428.782

**My question:** 
Africa is a continent why is it still reflected under countries 

Both entries for africa are missing data in the same fields, why is that?

## 8. AI-literacy reflection

Name **2 concrete risks** of trusting an AI assistant's output about this
dataset (or any data question) without checking it yourself. Then state
**one specific personal rule** for when you'll double-check an AI-provided
fact before relying on it professionally — specific enough that you could
actually follow it, not "I'll be careful."

**Risks:**
1. One risk would be the AI output would be inaccurate or distorted. Because, the data quality is poor, it may be hard for the AI to have context for mistakes or missing values
2. Another risk is hallucination, the AI may correlate things incorrectly and come to unreliable/innacurate conclusions. 

**My rule:** Always make sure the data set is clean and data quality is high before pushing to AI

## 9. Something that went wrong (and how you figured it out)

Somewhere in this project you're going to run a command that either throws
an error or gives you output that isn't what you expected — everyone hits
this at least once. Paste the actual command and what actually happened
(not a paraphrase), then explain what that told you and how it led to the
fix — not "I googled it and it worked."

```bash
awk -F',' '{print $1,$2,$3,$4,$5,$6}' co2_emissions_2022.csv | head -n 7
```

**What happened:**
This gave me the most issues, initially I did not add a space between the pipe and head, there was no error but the terminal continuously said "pipe>", Then I wanted 6 rows of data but when I put "head -n 6 only the first 5 were printed. 

**What it told me and how I fixed it:The header was included as a line. I then changed to 7 to include the header and print 6 lines of data for each country
