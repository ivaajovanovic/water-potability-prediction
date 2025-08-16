Water Potability Prediction using Machine Learning

This project is a comprehensive machine learning task aimed at predicting whether a water sample is potable (safe for human consumption) based on its chemical and physical properties. It follows a structured workflow from data exploration and preprocessing to model training, hyperparameter tuning, and final evaluation.

This project was completed as a requirement for the "Machine Learning 1" course.

🎯 Project Goal

The primary objective is to build and evaluate several classification models to accurately classify water samples. The project explores the effectiveness of different algorithms, the impact of dimensionality reduction, and the importance of hyperparameter tuning to find the best possible solution for this classification problem.

💾 Dataset

The dataset used in this project is the Water Potability Dataset, sourced from Kaggle.

Source: Kaggle Water Potability Dataset

Characteristics:

Instances: 3276

Features: 9 numerical input features (ph, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic_carbon, Trihalomethanes, Turbidity).

Target Variable: Potability (1 for Potable, 0 for Not Potable).

Challenges: The dataset contains a significant number of missing values and outliers, which require careful preprocessing. The classes are also slightly imbalanced.

📂 Project Structure

The repository is organized into a series of Jupyter Notebooks that follow the machine learning workflow chronologically:

01_data_exploration.ipynb: Contains the initial Exploratory Data Analysis (EDA), including statistical summaries, visualizations of feature distributions, outlier detection using boxplots, and correlation analysis.

02_data_preprocessing.ipynb: Handles all data cleaning and preparation steps. This includes imputing missing values, handling outliers using the capping method, and saving the final clean dataset (water_potability_clean.csv).

03_logistic_regression.ipynb: Implements, tunes, and evaluates the baseline model, Logistic Regression.

04_knn_classifier.ipynb: Implements, tunes, and evaluates the k-Nearest Neighbors (k-NN) classifier.

05_svm_classifier.ipynb: Implements, tunes, and evaluates the Support Vector Machine (SVM) classifier. This notebook also contains the final comparison of all models.

water_potability_clean.csv: The output of the preprocessing notebook, used as input for all model training notebooks.

requirements.txt: A list of all Python libraries required to run the project.

🛠️ Methodology

The project was executed following these key steps:

Exploratory Data Analysis (EDA): Initial analysis revealed that the problem is complex and non-linear, with no single feature strongly correlating with water potability.

Data Preprocessing:

Missing Value Imputation: Missing values in ph, Sulfate, and Trihalomethanes were filled using the mean of their respective target class (Potability 0 or 1) to preserve data distribution.

Outlier Handling: A "capping" method was applied, replacing extreme values below the 1st percentile and above the 99th percentile with the percentile value itself. This reduces the impact of outliers without data loss.

Data Splitting: The clean dataset was split into an 85% training set and a 15% testing set. This split was found to be optimal after experimenting with other ratios (80/20, 90/10).

Modeling & Hyperparameter Tuning: Three different classification algorithms were trained and evaluated:

Logistic Regression (Linear Baseline)

k-Nearest Neighbors (Non-linear)

Support Vector Machine with RBF Kernel (Non-linear)

For each model, GridSearchCV with 5-fold cross-validation was used to find the optimal set of hyperparameters.

Dimensionality Reduction: The impact of dimensionality reduction was tested for each model using two techniques:

LDA (Linear Discriminant Analysis): A supervised technique.

PCA (Principal Component Analysis): An unsupervised technique.

📊 Results

After thorough training and evaluation on the independent test set, the performance of the best version of each model was compared. The final results were obtained using the optimal 85/15 train/test split.

Metric (for Class 1 - Potable)	Logistic Regression	k-NN Classifier	Support Vector Machine (SVM)
Accuracy	~61%	~63%	~67%
F1-Score	0.00	0.31	0.41
Precision	0.00	0.56	0.71
Recall	0.00	0.22	0.29
Dimensionality Reduction	No Improvement	Worsened Results	Worsened Results

🏁 Conclusion

Best Model: The Support Vector Machine (SVM) with an RBF kernel proved to be the most effective model for this classification task, achieving the highest accuracy (67%) and, more importantly, the highest F1-Score (0.41) for the minority class.

Problem Nature: The failure of the linear model (Logistic Regression) and the success of the non-linear models (k-NN and SVM) confirm the initial EDA finding that the relationship between water properties and potability is highly complex and non-linear.

Impact of Dimensionality Reduction: For the powerful non-linear models, dimensionality reduction (both LDA and PCA) did not improve performance. This suggests that the subtle, non-linear information contained within the original 9 features was crucial for the models' success.

🚀 How to Run the Project

To replicate the results, follow these steps:

Clone the repository:

git clone https://github.com/ivaajovanovic/water-potability-prediction.git
cd water-potability-prediction

Create and activate a virtual environment:

python -m venv venv
# On Windows
.\venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate

Install the required libraries:
Run the Jupyter Notebooks in order:

Start with 01_data_exploration.ipynb.

Run 02_data_preprocessing.ipynb to generate the water_potability_clean.csv file.

Finally, you can run 03_..., 04_..., and 05_... to train and evaluate the models.
