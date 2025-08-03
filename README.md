# Apartment Rent Price Prediction

**Tools:** Python  
**Visualizations:** Seaborn, Matplotlib, Folium  
**Dataset:** Proprietary rental listing dataset (~10K rows)

---

## I. Business Problem Understanding

Accurate rental pricing is a crucial challenge in real estate. Overpricing leads to long vacancy, while underpricing results in lost income. Manual pricing is subjective and inconsistent across agents and regions.

### Problem Statement
- **Agent/Seller View:** Need data-driven tools to set optimal rent prices.
- **Buyer View:** Require fair pricing to guide decisions.
- **Platform View:** Require automated price suggestions to improve listing quality.

### Goals
1. Predict apartment rental prices using property features and location.  
2. Identify the most influential features affecting rent.  
3. Automate price estimation for listing platforms and agents.

### Business Impact
- Reduced pricing errors and faster listing decisions.  
- Enhanced user trust and engagement on rental platforms.  
- Data-driven pricing insights for agents and property owners.

---

## II. Data Understanding & Preprocessing

### Key Steps
- **Dropped uninformative columns:** `title`, `body`, `currency`, etc.  
- **Time Features:** Extracted `year`, `month`, `dayofweek` from timestamps.  
- **Missing Handling:**  
  - Categorical missing values like `pets_allowed` → "Unknown".  
  - Dropped rows missing core numeric data like `bedrooms`.  
- **Feature Engineering:**  
  - Extracted 30+ amenities into binary columns.  
  - Created `geo_cluster` using KMeans on lat-long.  
- **Categorical Grouping:** Simplified rare values (e.g. source, category).  
- **Scaling:**  
  - `RobustScaler` for `square_feet`,  
  - `MinMaxScaler` for bounded variables.

---

## III. Modeling

### Models Tested
- Linear Regression  
- KNN  
- Decision Tree  
- Random Forest  
- XGBoost  

All models used **log-transformed target (price)** to address skewness.

### Best Model
- **XGBoost Regressor**

### Performance on Test Set
| Metric | Value |
|--------|-------|
| RMSE   | ~359  |
| MAE    | ~222  |
| MAPE   | ~15.3% |

### Feature Importance (Top Predictors)
- `bedrooms`  
- `longitude`  
- `square_feet`  
- `amenity_Gym`  
- `pets_allowed`  

---

## IV. Conclusion and Recommendations

### Conclusion
- XGBoost showed best performance without need for tuning.  
- Price is influenced mainly by space (bedrooms, size), location, and key amenities.  
- Pet policies and listing platforms also affect price variation.

### Recommendations
- **Listing Platforms:** Embed model for auto-pricing on new listings.  
- **Agents/Owners:** Highlight top value-adding features (e.g. gym, AC).  
- **Product Team:** Build price suggestion dashboards using this model.

---

## V. Next Steps

- Incorporate listing engagement (views, inquiries) for behavioral insights.  
- Include macro factors (e.g. inflation, seasonal effects) in modeling.  
- Deploy as pricing microservice via API or dashboard module.  
