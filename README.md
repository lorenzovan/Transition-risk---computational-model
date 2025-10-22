# 🏛️ Computational Model for Transition Risk Capital Buffer

## 💡 Introduction

This repository holds the code and analysis developed for the **Master's Research Thesis** by **Lorenzo van Cadsand**.

The primary objective of this project is to **define a capital buffer for transition risk based on a simulation approach, applying VaR as risk measure to the empirical transition risk loss distribution.**

The core of the analysis and simulation is contained within the **Jupyter Notebook**.

---

## ⚙️ Key Parameters

The simulation relies on a set of critical parameters, which are defined and controlled within the main Jupyter Notebook. Understanding these parameters is essential for running the model:

| Parameter Name | Description |
| :--- | :--- |
| `num_simulations` | The total number of Monte Carlo simulations to be executed for the VaR calculation. --> in my model = 10.000|
| `max_subsectors_per_sector` | The maximum number of sub-sectors considered within each primary economic sector in the model. --> in my model = 3|
| `max_percentages` | This parameter indicates the maximum allowed percentage of fossil fuel or renewable energy production exposure within the simulated portfolios.--> must sum to 100.|
| `percentile` | The percentile considered for the empirical distribution of Transition Risk losses for the VaR calculation. |

---

## 📊 Data & Results Structure

The results and analysis are structured to allow for both regional and global assessments of the transition risk add-on.

### Regional Analysis

Results for specific geographic regions are obtained by analyzing the dedicated input files:

* **`shock_region`**: Contains the shock data specifically tailored to the regional economic and policy environment, obtained by the LIMITS database. 
* **`portfolio_region`**: Contains the portfolio exposure data for institutions focusing solely on a specific region, where assets/ liabilities/ LGD are simulated according to Gordy's.

To run the simulation you can use the csv file contained in the repository. 

### Global Portfolio Analysis

Results for global portfolios (those with exposure across multiple regions) are derived from the following input and output files:

* **`portafogliosimulazioni copia`**: The input file detailing the composition and exposure of the globally diversified portfolios used in the simulation.
* **`shock_results_final(in).csv`**: The output file containing the final simulated shock results, used as the primary input for the final VaR and capital buffer calculations.

Actual global exposure in uploaded portfolio is: 35% North America, 20% Europe, 20% Asia, 10% South America, 10% Africa, 5% Rest of the world (Oceania).

---

## ▶️ Running the Model

The analysis and simulation scripts are located in the main notebook.

1.  **Dependencies:** Ensure all required Python dependencies are installed (e.g., via a `requirements.txt` file).
2.  **Launch Jupyter:** Open your terminal in the project folder and start the Jupyter environment:
    ```bash
    jupyter notebook
    ```
    (or `jupyter lab`)
3.  **Execute:** Open the file **`Gitversion-tesi.ipynb`** and run all cells in sequential order to replicate the full analysis and generate the capital buffer results.

---

## 📧 Contact

* **Author:** Lorenzo van Cadsand
* **Affiliation:** Master's Research Thesis - Transition Risk Add-on: a Simulation Approach
* **Contact:** Lorenzovancadsand2@gmail.com
