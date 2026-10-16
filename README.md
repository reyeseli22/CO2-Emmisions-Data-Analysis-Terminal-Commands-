

# Climate and Energy Dataset Analysis

## 1. Scenario & Questions

A climate-and-energy nonprofit is seeking to determine where to direct its community-protection and climate-support efforts. To help inform these decisions, the organization has received a country-level energy and emissions dataset.

Our objective was to examine the dataset, understand its structure, and assess its quality and reliability before using it to inform decisions that could directly impact communities.

During our initial inspection, we sought to answer several questions:

- What does each column contain, and what data type does it represent?
- Is the dataset structured or unstructured?
- Are there missing values, suspicious entries, or inconsistencies that should be considered before using the data?
- How reliable is the dataset in helping us determine which communities may need the most support?

## 2. Dataset Overview

The dataset contains country-level information related to population, economic activity, and carbon dioxide emissions.

We observed six columns within the dataset:

| Column | Data Type | Description |

Country - string - Identifies country  

Iso code - string - Identifies country in "ABC" format

Year - Integer - Represents the year in which the data was recorded

Population - Integer - Represents the population of respective country

GDP -  Float - Represents the gross domestic product of a country or region.

Co2 - Float - Represents carbon dioxide emissions in a particlar country.

**Dataset Structure**

The dataset is structured, as we are able to navigate the information through predefined columns and rows. However, despite its organized structure, there are serious questions regarding its overall quality and completeness. These inconsistencies may be the result of issues during the data collection or processing stages.



## 3. What I Found

Throughout our initial inspection, we identified several observations that raise questions about the dataset's reliability. One of the most significant was missing data

One of the most significant findings was the substantial number of missing values throughout the dataset.

We observed a total of 125 missing fields across two columns:

- Iso Code : 36 missing values
- GDP 89 : missing values

Beyond these two columns, there is also a significant amount of missing information throughout the remainder of the dataset.

These missing values raise concerns about the dataset's completeness and whether it can effectively inform decisions regarding community-protection and climate-support efforts.

**Geographic Classification**

Another observation was the presence of continents, such as Africa and Asia, within the `country` column.

These regions appeared multiple times throughout the dataset, raising questions about how the data was collected, categorized, and organized.

Although the column is labeled country, it appears to contain information representing both countries and continents.

This distinction is important because it could affect how we interpret and compare the information.

## 4. Data Quality Question

While examining the dataset, several questions emerged regarding its quality and reliability.

The question I would prioritize asking the data provider is:

Does the dataset intentionally include both individual countries and continental aggregates within the country column?

I chose this question because we observed several instances where continents, including Africa and Asia, were listed alongside individual countries.

Understanding whether these entries are intentional would help clarify how the dataset was organized and whether the information can be compared accurately.

 This causes me to further question how reliable this dataset will be in effectively informing decisions regarding community-protection and climate-support efforts, especially given the significant amount of missing information.

Before drawing conclusions, it is important for us to understand the methods used to collect and organize the data.

## 5. Reflection

Personally, I am interested in exploring the underlying reasons why so many fields within the dataset are missing information.

I am also interested in understanding how the different data types and variables intersect, and how analyzing their relationships could allow us to develop a greater understanding of where support is most needed.

This initial exploration reinforced the importance of questioning the quality and reliability of data before using it to inform real-world decisions.

**AI-Literacy Takeaway**



I generally did not use AI in order to inspect this data set. The extent of my use of AI within this project 1. to understand and utilize terminal command to analyze ther data set and 2. Organizing my thoughts and reflections into a more organized and digestable way