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

## License
This project is for academic purposes as part of the Master's in AI.

 
Update: Documentation finalized for submission 
