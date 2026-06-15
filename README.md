# 🛍️ Customer Personality Analysis — Unsupervised Learning

An unsupervised machine learning project that segments a retail company's customer base into distinct groups using clustering, then translates those segments into actionable marketing strategies.

## 📌 Project Overview

Understanding customers at a granular level allows a business to tailor products, offers, and communication to the people most likely to respond. This project applies **dimensionality reduction (PCA)** and **clustering (Agglomerative Clustering / K-Means)** to a marketing campaign dataset, identifying **4 distinct customer segments** based on demographics, household composition, income, and spending behavior.

## 🎯 Objectives

- Clean and preprocess raw customer data (handle missing values, outliers, encoding).
- Engineer meaningful features (age, total spend, family size, parental status, tenure).
- Reduce dimensionality with PCA for efficient and meaningful clustering.
- Determine the optimal number of clusters using the Elbow Method.
- Segment customers using Agglomerative Clustering.
- Profile each cluster and visualize spending/income/promotion patterns.
- Translate cluster profiles into targeted marketing recommendations.

## 🗂️ Dataset

The dataset (`marketing_campaign.csv`) contains customer records including:

- **Demographics:** `Year_Birth`, `Education`, `Marital_Status`, `Income`
- **Household:** `Kidhome`, `Teenhome`
- **Customer relationship:** `Dt_Customer`, `Recency`
- **Spending:** `MntWines`, `MntFruits`, `MntMeatProducts`, `MntFishProducts`, `MntSweetProducts`, `MntGoldProds`
- **Campaign response:** `AcceptedCmp1–5`, `Response`, `Complain`
- **Purchase channels:** `NumDealsPurchases`, `NumWebPurchases`, `NumCatalogPurchases`, `NumStorePurchases`, `NumWebVisitsMonth`

## 🛠️ Tech Stack

- **Python 3**
- **pandas / numpy** — data manipulation
- **matplotlib / seaborn** — visualization
- **scikit-learn** — `LabelEncoder`, `StandardScaler`, `PCA`, `AgglomerativeClustering`, `KMeans`, `metrics`
- **yellowbrick** — `KElbowVisualizer` for optimal cluster selection

## 🔄 Workflow

1. **Data Cleaning**
   - Drop rows with missing values (`Income`).
   - Remove outliers (`Age > 90`, `Income > 600,000`).

2. **Feature Engineering**
   - `Age` = current year − `Year_Birth`
   - `Spent` = sum of all product spending columns
   - `Living_With` = simplified marital status (`Partner` / `Alone`)
   - `Children` = `Kidhome` + `Teenhome`
   - `Family_Size` = household size based on `Living_With` + `Children`
   - `Is_Parent` = 1 if `Children > 0`, else 0
   - `Customer_For` = days since enrollment (relative to most recent customer)
   - `Education` simplified into `Undergraduate`, `Graduate`, `Postgraduate`

3. **Preprocessing**
   - Label-encode categorical features.
   - Drop campaign-acceptance columns prior to scaling (kept aside for post-clustering analysis).
   - Standardize all features with `StandardScaler`.

4. **Dimensionality Reduction**
   - Apply **PCA** to reduce the scaled feature set to **3 principal components**.
   - Visualize the data in 3D to inspect underlying structure.

5. **Clustering**
   - Use the **Elbow Method** (`KElbowVisualizer`) on the PCA-reduced data to determine the optimal number of clusters → **4**.
   - Apply **Agglomerative Clustering** with `n_clusters=4`.

6. **Cluster Evaluation & Visualization**
   - 3D scatter plot of clusters in PCA space.
   - Cluster size distribution.
   - Income vs. Spending scatter plot by cluster.
   - Spending distribution per cluster (swarm + boxen plots).
   - Promotion acceptance and deals-purchased patterns per cluster.
   - Joint distribution plots of personal attributes (age, family size, parental status, education, etc.) vs. spending, by cluster.

## 👥 Customer Segments

### Cluster 0 — The Older Family Household
- Definitely a parent (single or partnered)
- Family size: 2–4 members
- Most have a teenager at home
- Relatively older demographic

**Strategy — Convenience & Family Value Packs**
- Multi-buy discounts (e.g., "Buy 2, Get 1 Free") on household staples like cereals, snacks, and cleaning supplies.
- Promote ready-made meal kits designed for 3–4 people.
- Use traditional channels (flyers, newspaper inserts) alongside digital ads.

### Cluster 1 — The Younger Parent Family
- Majority are parents
- Family size: up to 3 members
- Typically one young child (not a teenager)
- Relatively younger demographic

**Strategy — Child-Centric, Premium & Easy**
- Highlight fresh produce and organic baby/toddler items.
- Run targeted social media ads and app-based personalized coupons.
- Offer in-store experiences like "kids eat free" samples and family-friendly parking.

### Cluster 2 — The High-Income Non-Parent
- Not a parent
- Household of 1–2 members; slight majority are couples
- Spans all ages
- High-income group

**Strategy — Premium, Specialty & Gourmet**
- Promote high-end cuts of meat, imported cheeses, fine wines, and specialty/international foods.
- Create premium bundle kits (e.g., "Gourmet Pasta Night") emphasizing quality over savings.
- Use elegant, magazine-style email newsletters to showcase exclusive products.

### Cluster 3 — The Budget-Conscious Large Family
- Definitely a parent
- Family size: 2–5 members
- Majority have a teenager at home
- Relatively older, lower-income group

**Strategy — Maximize Savings & Volume Discounts**
- Prioritize store-brand/private-label products across all categories.
- Promote bulk-buying options and publicize weekly circular sales.
- Implement a high-value loyalty program with points or cash-off rewards.

## 💡 Key Takeaway

Each cluster demands a distinct marketing approach — from gourmet experiences for Cluster 2 to bulk savings for Cluster 3. A one-size-fits-all strategy leaves money on the table; tailored campaigns unlock maximum engagement and loyalty.

## 🚀 How to Run

1. Place `marketing_campaign.csv` in the working directory (update the file path in the notebook if needed).
2. Install dependencies:
   ```bash
   pip install numpy pandas matplotlib seaborn scikit-learn yellowbrick
   ```
3. Open and run `Unsupervised_Learning_Project_2.ipynb` cell by cell in Jupyter Notebook / JupyterLab.

## 📁 Project Structure

```
.
├── Unsupervised_Learning_Project_2.ipynb   # Main analysis & clustering notebook
├── Profiling-the-Customer-Clusters.pdf     # Cluster profiles & marketing strategy deck
└── README.md                               # Project documentation
```
