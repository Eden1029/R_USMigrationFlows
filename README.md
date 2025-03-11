# 🏡 U.S. Migration Flows Analysis (2010-2019) - R Project  

## 📌 Overview  
This **R-based data analysis project** explores **domestic and international migration flows across U.S. states from 2010 to 2019**.  
The project aims to **analyze migration trends, patterns, and insights** to better understand **state-to-state and international migration movements**.  

Using **data visualization techniques in R (ggplot2 package)**, this project presents:  
✅ **Total migration trends over time (2010-2019)**  
✅ **State-level migration inflows and outflows**  
✅ **Comparison of domestic vs. international migration**  
✅ **Correlation analysis between population size and migration inflows**  

---

## 📂 Dataset Details  
This project uses the **US Migration Flows in 10 Years dataset**, which consists of:  

1. **Migration_Flows_from_2010_to_2019.csv**  
   - **Contains yearly migration data across U.S. states**.  
   - **Key columns:**  
     - `year` - Year of migration  
     - `original_region` - Origin state  
     - `current_state` - Destination state  
     - `number_of_people` - Number of people migrated  
     - `abroad_Total` - Migration from foreign countries  
     - `from_different_state_Total` - Migration from other U.S. states  

2. **R_Migration Flows Project.R**  
   - **R script containing all data processing, analysis, and visualization steps**.  

---

## 🏗️ Data Processing & Key Analysis Steps  

### ✅ **1. Data Import & Preprocessing**  
- The dataset is loaded using the **read_csv()** function.  
- Column `from` is renamed to `original_region` to avoid confusion.  
- Data cleaning steps include:
  - Checking for missing values and duplicates.
  - Exploring the dataset using `head()`, `tail()`, `summary()`, and `str()` functions.  

```r
library(readr)
library(dplyr)

USdata <- read_csv("Migration_Flows_from_2010_to_2019.csv")
colnames(USdata) <- rename(original_region = from)
sum(is.na(USdata))  # Check missing values
sum(duplicated(USdata))  # Check duplicate rows
```

---

### ✅ **2. Data Aggregation**  
✅ **Time Aggregation:**  
- Total number of migrants calculated per year (2010-2019).  
✅ **Spatial Aggregation:**  
- Total migrants per U.S. state.  
- Domestic vs. international migration analysis.  

```r
yearly_migration <- USdata %>%
  group_by(year) %>% 
  summarise(yearly_total_migrants = sum(number_of_people, na.rm = TRUE))
```

---

## 📊 Data Visualization & Insights  

### 1️⃣ **Line Chart: Total U.S. Migration Trends (2010-2019)**  
✅ **Illustrates annual migration trends over time.**  

```r
ggplot(yearly_migration, aes(x = factor(year), y = yearly_total_migrants, group = 1)) +
  geom_point(color = "blue") + 
  geom_line(color = "skyblue") +
  labs(title = "US Migration by Year (2010 - 2019)",
       x = "Year",
       y = "Total Migrants") +
  scale_y_continuous(labels = scales::comma) +
  theme_minimal()
```

📊 **Findings:**  
- **Migration peaked in 2016 but declined afterward**.  
- The decline **coincides with U.S. immigration policy changes in 2017**.  

---

### 2️⃣ **Bar Chart: Migration by State**  
✅ **Highlights the states receiving the highest number of migrants.**  

```r
state_migration <- USdata %>%
  group_by(current_state) %>%
  summarise(state_total_migrants = sum(number_of_people, na.rm = TRUE))

ggplot(state_migration, aes(x = state_total_migrants, y = current_state)) +
  geom_bar(stat = "identity", fill = 'royalblue2') +
  labs(title = "US Migration by State",
       x = "Total Migrants",
       y = "State") +
  scale_x_continuous(labels = scales::comma) +
  theme_minimal()
```

📊 **Findings:**  
- **California, Texas, and Florida receive the most migrants**.  
- **States with lower job opportunities see lower migration rates**.  

---

### 3️⃣ **Heatmap: Migration by Year & State**  
✅ **Shows migration density using colors to indicate migration levels.**  

```r
heatmap_YearState <- ggplot(year_state_migration, aes(x = factor(year), y = current_state, fill = total_migrants)) +
  geom_tile(color = "black") +  
  scale_fill_gradient(low = "lightblue", high = "darkblue") +  
  labs(title = "Total Migrants by Year and State",
       x = "Year",
       y = "State") +
  theme_minimal()
```

📊 **Findings:**  
- **Texas and Florida consistently gain migrants, while some states lose population**.  
- **Migration levels are highly influenced by economic conditions**.  

---

### 4️⃣ **Scatter Plot: Relationship Between Population & Migration**  
✅ **Analyzes correlation between state population size and international migration.**  

```r
ggplot(USdata, aes(x = population, y = abroad_Total)) +
  geom_point(color = "darkblue") +  
  geom_smooth(method = "lm", color = "red", se = TRUE) +
  labs(title = "Population vs. Abroad Migration",
       x = "Population",
       y = "Abroad Migrants") +
  theme_minimal()
```

📊 **Findings:**  
- **Larger states tend to receive more international migrants**.  
- **There is a strong positive correlation between population and migration inflows**.  

---

## 🎨 **Design & Customization**  
- **Color choices help distinguish domestic vs. international migration trends.**  
- **Minimalist themes (theme_minimal()) are used to avoid clutter.**  
- **Annotations and labels added to improve readability.**  

---

## 🔍 **Key Insights & Findings**  

📌 **Overall Migration Trends:**  
- **Migration increased from 2010 to 2016, then declined sharply from 2017 to 2019.**  
- The **decline corresponds with U.S. immigration policies introduced in 2017**.  

📌 **State-Level Migration Trends:**  
- **California attracts the most international migrants,** while **Texas and Florida attract more domestic migrants**.  
- **New York and Illinois experience more out-migration** due to **high living costs**.  

📌 **Domestic vs. International Migration:**  
- **Domestic migration trends show people moving towards Republican states (Texas, Florida).**  
- **International migrants prefer Democratic states like California and New York.**  

📌 **Economic & Policy Impacts on Migration:**  
- **Migration trends are strongly influenced by job availability and political policies**.  
- **Red states (Texas, Florida) balance migration and economic growth, while blue states (California, New York) face higher out-migration.**  

---

## 🚀 Future Improvements  
🔹 **Use predictive modeling to forecast migration patterns.**  
🔹 **Analyze how job opportunities impact migration trends.**  
🔹 **Expand analysis to include education and economic factors.**  

---

## 🤝 Connect with Me  
📧 **Email:** eden.vietnguyen@gmail.com  
🔗 **LinkedIn:** [www.linkedin.com/in/eden-nguyen](https://www.linkedin.com/in/eden-nguyen)  
🌐 **Portfolio Website:** [eden-nguyen.vercel.app](https://eden-nguyen.vercel.app/)  

