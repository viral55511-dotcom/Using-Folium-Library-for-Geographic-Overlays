# 🌍 PROJECT : Geographic Visualization of CO₂ Emissions Using Folium

## 📌 Overview

This project focuses on **visualizing global CO₂ emissions per capita** using interactive maps built with the Folium library.

Using the **World Development Indicators dataset**, we explore how carbon emissions vary across countries and present the data through a **choropleth map**.

---

## 📂 Dataset

* **Source:** World Bank – World Development Indicators
* **File:** `Indicators.bz2` (compressed dataset)
* **Content Includes:**

  * Country Name & Code
  * Indicator Name
  * Year
  * Indicator Value

---

## 🛠️ Technologies Used

* Python
* Pandas
* Folium
* Jupyter Notebook

---

## 🎯 Project Objective

* Analyze **CO₂ emissions per capita (2011)**
* Map emissions geographically
* Create **interactive visualizations**

---

## 📥 Data Loading

```python
import pandas as pd

data = pd.read_csv('data/Indicators.bz2', compression='bz2')
print(data.shape)
print(data.head())
```

---

## 🔍 Data Filtering

### Select CO₂ emissions for all countries in 2011:

```python
hist_indicator = r'CO2 emissions \(metric'
hist_year = 2011

mask1 = data['IndicatorName'].str.contains(hist_indicator, na=False)
mask2 = data['Year'] == hist_year

stage = data[mask1 & mask2]
```

---

## 📊 Prepare Data for Mapping

```python
plot_data = stage[['CountryCode', 'Value']]
hist_indicator = stage.iloc[0]['IndicatorName']
```

---

## 🌍 Choropleth Map Visualization

### Create Interactive Map:

```python
import folium

m = folium.Map(location=[20, 0], zoom_start=2)

folium.Choropleth(
    geo_data='data/world-countries.json',
    data=plot_data,
    columns=['CountryCode', 'Value'],
    key_on='feature.id',
    fill_color='YlGnBu',
    fill_opacity=0.7,
    line_opacity=0.2,
    legend_name=hist_indicator
).add_to(m)

m.save('saved_info/plot_data.html')
```

---

## 📺 Display Map in Notebook

```python
from IPython.display import HTML

HTML('<iframe src=saved_info/plot_data.html width=700 height=450></iframe>')
```

---

## 🌟 Key Features

* 🌍 Interactive world map
* 📊 CO₂ emissions comparison by country
* 🎯 Year-specific analysis (2011)
* 📈 Visual storytelling

---

## ⚠️ Challenges Faced

* Handling compressed `.bz2` dataset
* Fixing **regex escape sequence issues**
* Updating deprecated Folium method (`choropleth`)
* Managing GeoJSON file paths

---

## ✅ Key Learnings

* Data filtering using Pandas
* Working with geospatial data
* Building interactive maps using Folium
* Debugging real-world dataset issues

---

## 🚀 Future Improvements

* Add multiple years comparison
* Include GDP overlay
* Add hover tooltips with country names
* Build dashboard using Power BI or Streamlit

---

## 📌 Conclusion

This project demonstrates how **data + geography = powerful insights**.
Using Folium, we transformed raw CO₂ data into an **interactive global visualization**, making trends easy to understand and analyze.

---

## 👤 Author

**Viral Parmar**
Data Analyst | Python | Power BI | SQL

---

## ⭐ Support

If you like this project, give it a ⭐ on GitHub!
