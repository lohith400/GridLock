Traffic Demand Prediction - Gridlock Hackathon 2.0
📁 Directory Structure
To reproduce the results, the files should be organized as follows:

Plaintext
📂 Project_Folder
 ┣ 📜 main_model.py          # (Or .ipynb) The final Python code provided
 ┣ 📜 README.md              # This explanation document
 ┗ 📂 dataset                # The data directory
    ┣ 📜 train.csv           # Training data provided by HackerEarth
    ┣ 📜 test.csv            # Test data provided by HackerEarth
    ┗ 📜 submission.csv      # The final generated output file
🧠 Methodology & Approach
The goal of this project is to accurately predict traffic demand based on time, location (geohash), weather, and road conditions. To achieve a highly optimized score, the approach relied heavily on Advanced Feature Engineering and Ensemble Modeling.

1. Feature Engineering
Instead of passing raw data into the model, several transformations were applied to extract deeper patterns:

Cyclical Time Transformation: Raw timestamps (HH:MM) are difficult for machine learning models to interpret continuously (e.g., the model doesn't inherently know that 23:59 and 00:01 are only two minutes apart). To solve this, time was converted into total daily minutes, and then mapped onto a circle using Sine and Cosine functions. This perfectly preserves the cyclical nature of a 24-hour day.

Smoothed Target Encoding (Geohash): The geohash variable is highly cardinal (contains many unique locations). Standard categorical encoding is inefficient here. Instead, Target Encoding was utilized to replace each geohash with its historical average traffic demand. A mathematical smoothing factor (weight) was applied to prevent overfitting on locations that had very few historical data points.

Frequency Encoding:
The total historical frequency of each geohash was calculated to give the model a sense of how "busy" or common a specific location is within the dataset.

2. Data Preprocessing
Missing categorical variables (such as Weather, Landmarks, or RoadType) were explicitly filled with a 'Missing' placeholder so the model could learn patterns even when data was absent.

The OrdinalEncoder was strictly configured to handle unknown values gracefully (handle_unknown='use_encoded_value'). This ensures that if the test set introduces a completely new location or weather condition not seen in training, the pipeline will not crash.

3. Modeling Strategy
Algorithm: LightGBM (Light Gradient Boosting Machine) was selected as the core estimator. It natively handles categorical features, builds trees highly efficiently, and is the industry standard for tabular data regression tasks.

K-Fold Cross Validation (Ensembling):
To maximize generalization and achieve the highest possible accuracy, a 5-Fold Cross Validation strategy was implemented. Instead of training one model, the data was split into 5 distinct slices.

Five separate LightGBM models were trained, each evaluating a different section of the data.

The final predictions submitted in submission.csv are the averaged predictions of all 5 models. This ensemble method drastically reduces variance and model bias, resulting in a highly robust predictive engine.


