# 🚧 Road Condition Classification using Surface Distress Index (SDI)
This project classifies road conditions based on the **Surface Distress Index (SDI)**, which is calculated using various road damage indicators such as cracks, potholes, and ruts.

## 📌 Overview
The classification is based on different types and levels of road damage, with assigned weights to compute the **SDI score**. The final road condition is categorized as:
- **Baik (Good)**
- **Sedang (Moderate)**
- **Rusak Ringan (Slightly Damaged)**
- **Rusak Sedang (Moderately Damaged)**
- **Rusak Berat (Severely Damaged)**

## 📊 Data Used
The dataset includes road damage attributes for multiple road sections:
- **Cracks (Light, Moderate, Severe)**
- **Potholes (Light, Severe)**
- **Rutting (Deformation)**

Example of input data:
| Ruas Jalan | Retak Ringan | Retak Sedang | Retak Berat | Lubang Ringan | Lubang Berat | Alur |
|------------|-------------|-------------|-------------|--------------|-------------|------|
| A1         | 5           | 3           | 1           | 2            | 0           | 1    |
| A2         | 2           | 4           | 0           | 1            | 1           | 0    |
| A3         | 8           | 2           | 3           | 0            | 2           | 1    |

## 🔍 How It Works
1. Each damage type is assigned a **weight** based on its severity:
   - Light Crack: `0.2`
   - Moderate Crack: `0.5`
   - Severe Crack: `0.8`
   - Light Pothole: `0.3`
   - Severe Pothole: `0.7`
   - Rutting: `0.4`
   
2. **SDI Calculation**  
   The SDI score is computed using the weighted sum of damage severity:
   ```python
   def calculate_sdi(row):
       weights = {
           'retak_ringan': 0.2,
           'retak_sedang': 0.5,
           'retak_berat': 0.8,
           'lubang_ringan': 0.3,
           'lubang_berat': 0.7,
           'alur': 0.4
       }
       return sum(row[col] * weights[col] for col in weights.keys())
   df['SDI'] = df.apply(calculate_sdi, axis=1)
   ```

3. **Condition Classification**  
   Based on the SDI score, roads are categorized into five conditions:
   ```python
   def klasifikasi_kondisi(sdi):
       if sdi < 2:
           return 'Baik'
       elif 2 <= sdi < 5:
           return 'Sedang'
       elif 5 <= sdi < 8:
           return 'Rusak Ringan'
       elif 8 <= sdi < 12:
           return 'Rusak Sedang'
       else:
           return 'Rusak Berat'
   df['kondisi'] = df['SDI'].apply(klasifikasi_kondisi)
   ```

## ✅ Results Example
| Ruas Jalan | SDI Score | Condition |
|------------|----------|-----------|
| A1         | 4.3      | Sedang |
| A2         | 3.4      | Sedang |
| A3         | 6.8      | Rusak Ringan |
| B1         | 6.7      | Rusak Ringan |
| B2         | 6.4      | Rusak Ringan |

## 🛠️ Requirements
To run this project, install the required libraries:
```sh
pip install pandas numpy
```

## 🚀 Run the Code
Run the Python Notebook:
```sh
jupyter notebook Road_Classification_SDI_1.ipynb
```

## 📌 Conclusion
This project provides a simple yet effective way to classify road conditions using the SDI method. This can be further extended with **machine learning models** or **GIS-based visualization**.

---

**Author:** _naziraayu_  
📌 _Follow for more data science projects!_

