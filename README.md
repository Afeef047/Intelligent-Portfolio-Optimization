# AI-Driven Portfolio Optimization

This project implements an end-to-end pipeline for portfolio optimization, built in Python. It uses a custom-trained **XGBoost** model (with **Focal Loss**) for transparent asset selection and the **Black-Litterman** model for robust, stable portfolio allocation.

This approach is designed to overcome the "black box" and instability problems found in traditional machine learning and Markowitz-based models.

## Core Features

* **Transparent AI:** Uses XGBoost, which is fully explainable with SHAP, to move beyond "black box" models like SVMs.
* **Specialized Training:** Implements a Focal Loss function to force the model to focus on rare "buy" signals.
* **Stable Allocation:** Replaces the unstable Markowitz model with the Black-Litterman model, which blends AI-driven views with stable market equilibrium.

## Project Pipeline

The pipeline is broken into modular scripts that must be run in order.

1.  **`Data_Generation.py`**: Downloads all raw stock data (Nifty 50, Euro Stoxx 50) from Yahoo Finance.
2.  **`Preprocess.py`**: Loads raw data, calculates 15 technical features (RSI, MACD, etc.), and saves a final processed dataset.
3.  **`Train_Test_Split.py`**: Loads the processed data, scales it using `StandardScaler`, and splits it into time-series-aware training/testing sets.
4.  **`Model_Train.py`**: Trains the XGBoost classifier using the custom Focal Loss function. Saves the final model.
5.  **`Black_Litterman_Model.py`**: Loads the trained model to generate "views" on the latest data and runs the Black-Litterman allocation.
6.  **`Benchmark.py`**: Contains functions to create baseline portfolios (Naive Markowitz, SVM-Markowitz) for comparison.
7.  **`Backtest_Analysis.py`**: Generates the final Efficient Frontier comparison graphs and performance metrics.
8.  **`SHAP.py`**: Runs SHAP analysis on the trained model to generate plots explaining *why* the AI makes its decisions.
9.  **`Dashboard.py`**: A Streamlit web application to display all the results interactively.

## Installation

1.  Clone the repository.
2.  (Recommended) Create a virtual environment:
    ```bash
    python -m venv venv
    venv\Scripts\activate
    ```

3.  Install all required libraries using the `requirements.txt` file:
    ```bash
    pip install -r requirements.txt
    ```

## How to Run the Pipeline

Run the scripts from your terminal in the following order:

1.  **Generate Data:**
    ```bash
    python Data_Generation.py
    ```

2.  **Process Data & Features:**
    ```bash
    python Preprocess.py
    ```

3.  **Split & Scale Data:**
    ```bash
    python Train_Test_Split.py
    ```

4.  **Train the AI Model:**
    ```bash
    python Model_Train.py
    ```

5.  **Generate Analysis & Graphs:**
    ```bash
    python Backtest_Analysis.py
    python SHAP.py
    ```

6.  **View the Interactive Dashboard:**
    ```bash
    streamlit run Dashboard.py
    ```
