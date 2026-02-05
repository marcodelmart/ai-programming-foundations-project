# NYC Airbnb Market Analysis Pipeline

**Author:** Marco Flavio Delgado Martinez
**Status:** Active
**Tech Stack:** Python, Pandas, Seaborn

## Project Description
This project implements a reproducible data engineering workflow to analyze the 2019 NYC Airbnb market. By ingesting and cleaning raw listing data, I explored the relationship between market saturation (listing volume) and pricing power across the five NYC boroughs. The goal is to provide data-driven insights for pricing optimization and identifying high-competition zones.

**Dataset:** [New York City Airbnb Open Data (Kaggle)](https://www.kaggle.com/dgomonov/new-york-city-airbnb-open-data)

## Project Structure
* data_workflow.ipynb: The main Jupyter Notebook containing the ingestion, cleaning, EDA, and visualization code.
* AB_NYC_2019.csv: The raw dataset (ensure this is in the root directory).
* requirements.txt: List of Python dependencies required to reproduce the environment.
* module_summary.pdf: Detailed report with academic citations and business interpretation.

## How to Run
1. Clone the repository:
   git clone https://github.com/marcodelmart/ai-programming-foundations-project.git
   cd ai-programming-foundations-project

2. Install Dependencies:
   pip install -r requirements.txt

3. Run the Analysis:
   Open data_workflow.ipynb in Jupyter Lab or VS Code and run all cells sequentially from top to bottom.

## Reproducibility and Bias Note
* **Bias:** Missing reviews were imputed with 0 to preserve new listings in the analysis. Availability data (0 days) is treated as-is but may represent inactive listings.
* **Cleaning:** Prices above the 99th percentile were removed to prevent skew in average price calculations.
* **Environment:** The requirements.txt file ensures the correct library versions are installed for exact reproducibility.

## Bias and Data Governance Considerations

**Missing Review Data Strategy**
My decision to impute missing values in `reviews_per_month` with 0 was driven by the business logic that "NaN" typically implies "Zero Reviews" for new listings.
* **Potential Bias:** This approach assumes that missing data is always informational (zero activity) rather than an error. If the data is missing due to a system failure, I might be underestimating the activity of established hosts.
* **Impact:** This decision benefits **New Hosts** by keeping them in the dataset. If I had dropped these rows (Alternative Approach), I would have introduced "Survivorship Bias," creating a dataset that only reflects successful, long-term hosts, thereby ignoring the entry barriers for new market participants.

**Price Outlier Removal**
I capped prices at the 99th percentile to prevent extreme outliers from skewing the average price analysis.
* **Potential Bias:** This decision explicitly excludes the **Ultra-Luxury Segment**. Consequently, my analysis is biased toward the "General Consumer Market."
* **Impact:** A luxury property manager using this model would find the price predictions inaccurate (too low). However, for 99% of users, the removal of these outliers results in a more robust and generalized insight.

## Future Integration Reflections

### Machine Learning Workflow Integration
If I were to extend this data workflow to a supervised Machine Learning pipeline to predict listing prices, I would implement the following steps:
1.  **Feature Engineering:** I would convert categorical variables like `neighbourhood_group` and `room_type` into numerical formats using One-Hot Encoding. I would also engineer a `distance_to_center` feature using the latitude and longitude coordinates.
2.  **Train/Test Split:** I would split the data (e.g., 80% training, 20% testing) ensuring a stratified split based on `neighbourhood_group` to maintain geographic representation in both sets.
3.  **Model Selection:** I would likely start with a Random Forest Regressor due to its ability to handle non-linear relationships and interactions between location and price.

### Neural Network Preparation
To prepare this dataset for a Deep Learning model, stricter preprocessing is required:
1.  **Normalization:** Neural networks require scaled inputs. I would apply `MinMaxScaler` or `StandardScaler` to continuous variables like `price`, `minimum_nights`, and `availability_365` to bring them within a 0-1 range.
2.  **Embeddings:** For high-cardinality categorical features like the specific `neighbourhood` column (which has over 200 unique values), One-Hot Encoding would create a sparse matrix. I would instead use an Embedding Layer to capture semantic relationships between neighborhoods.

### Agentic AI Automation Potential
An Agentic AI system could automate the governance and maintenance of this pipeline:
1.  **Automated Data Quality:** An agent could be deployed to monitor incoming data streams, automatically flagging rows where `price=0` or `availability=365=0` and generating a "Data Quality Report" for human review.
2.  **Bias Detection:** An agent could simulate "What-If" scenarios (e.g., "What if we drop nulls instead of imputing?") and automatically visualize the distribution shift, alerting the Data Engineer if a specific demographic (e.g., Bronx listings) is disproportionately affected by a cleaning rule.

## License
This project is for academic purposes as part of the Master's in AI.

Update: Documentation finalized for submission
