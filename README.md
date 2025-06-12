# Project Title
Responsible AI Toolkit for Fair Loan Prediction

# Description
This project is a web application designed to promote responsible AI practices in loan prediction. It provides tools to assess and mitigate bias in datasets, generate synthetic data using Generative Adversarial Networks (GANs), train fairer predictive models, and explain bias metrics in an understandable way. The goal is to help users build more equitable and transparent loan approval systems.

# Features
- Dataset uploading (CSV format).
- Automated data preprocessing, including handling missing values and encoding categorical features.
- Synthetic data generation using GANs to augment datasets and potentially reduce bias.
- Calculation and visualization of key bias metrics:
    - Disparate Impact
    - Statistical Parity Difference
- Comparison of bias metrics between original and augmented datasets.
- Training of a logistic regression model for loan prediction using the (potentially fairer) augmented data.
- Explanation of bias metrics and their implications using OpenAI's GPT-3.5-turbo.
- User-friendly web interface built with Flask.

# Technologies Used
- **Backend:** Python, Flask
- **Frontend:** HTML, CSS, JavaScript
- **Data Handling & ML:** pandas, NumPy, scikit-learn, TensorFlow/Keras
- **Fairness & Bias Detection:** AIF360
- **AI Explanations:** OpenAI API (GPT-3.5-turbo)
- **Plotting:** Matplotlib
- **Environment Management:** python-dotenv

# Setup and Installation
1.  **Clone the repository:**
    ```bash
    git clone <repository_url>
    cd <repository_directory>
    ```
2.  **Create and activate a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    *(Note: `aif360` is a comprehensive library. While the core metrics used in this toolkit are generally straightforward to install, some advanced functionalities of AIF360 might have additional system-level dependencies depending on your OS.)*
4.  **Set up Environment Variables:**
    Create a `.env` file in the root directory of the project and add your OpenAI API key:
    ```
    OPENAI_API_KEY='your_openai_api_key_here'
    ```
5.  **Run the application:**
    ```bash
    python responsible_ai_toolkit/app.py
    ```
    The application will be accessible at `http://127.0.0.1:5000/`.

# Usage
1.  **Navigate to the Homepage:** Open your web browser and go to `http://127.0.0.1:5000/`.
2.  **Upload Dataset:**
    - Click on the "Choose File" button under the "Upload Dataset" section.
    - Select your loan dataset in CSV format (e.g., `Loan_Train.csv`).
    - Click "Upload".
3.  **Preprocess Data:**
    - After uploading, click the "Preprocess Data" button.
    - This will handle missing values and encode categorical features. A confirmation message will appear.
4.  **Generate Synthetic Data & Analyze Bias:**
    - Click the "Generate Synthetic Data" button.
    - The application will train a GAN, generate synthetic samples, and save them.
    - Bias metrics (Disparate Impact, Statistical Parity Difference) for both original and combined (original + synthetic) data will be calculated.
    - Visualizations comparing data distributions and bias metrics will be generated and displayed. These can be found in the `responsible_ai_toolkit/static/plots/` directory.
5.  **Train Predictive Model:**
    - Click the "Train Model" button.
    - A logistic regression model will be trained using the combined (original + synthetic) data.
    - The accuracy of the model will be displayed.
6.  **Explain Bias:**
    - Click the "Explain Bias" button.
    - The application will send the calculated bias metrics to the OpenAI API.
    - An explanation of what these metrics mean, how synthetic data impacted fairness, and suggestions for improvement will be displayed.

# File Structure
```
.
├── Loan_Train.csv              # Example loan dataset
├── README.md                   # This file
├── requirements.txt            # Python package dependencies
└── responsible_ai_toolkit/
    ├── app.py                  # Main Flask application logic
    ├── data/
    │   ├── preprocessed_data.csv # Preprocessed data
    │   └── synthetic_data.csv  # Generated synthetic data
    ├── models/                 # (Currently contains .h5 and .pkl, though app.py seems to regenerate/train models on the fly)
    │   ├── gan_generator.h5    # Saved GAN generator model (if used for persistence)
    │   └── predictive_model.pkl# Saved predictive model (if used for persistence)
    ├── static/
    │   ├── plots/              # Directory for storing generated plot images
    │   │   ├── ApplicantIncome_comparison.png
    │   │   └── ... (other comparison plots)
    │   ├── script.js           # Frontend JavaScript
    │   └── style.css           # CSS styles for frontend
    ├── templates/
    │   ├── index.html          # Main HTML template for the application
    │   ├── results.html        # HTML template for displaying results (if used separately)
    │   └── style.css           # (Note: There's a style.css in this directory which might be unused or redundant if responsible_ai_toolkit/static/style.css is the primary stylesheet. Consider consolidating.)
    └── uploads/
        └── Loan_Train.csv      # Uploaded datasets are stored here
```

# Bias Metrics
The toolkit focuses on the following fairness metrics from the AIF360 library:
-   **Disparate Impact:** This is a ratio that measures the proportion of individuals in the unprivileged group who receive a favorable outcome compared to the proportion of individuals in the privileged group who receive a favorable outcome. A value close to 1 is desired. Values less than 0.8 or greater than 1.25 are often considered indicative of adverse impact.
    -   *Formula:* `P(favorable_outcome | unprivileged_group) / P(favorable_outcome | privileged_group)`
-   **Statistical Parity Difference (SPD):** This metric measures the difference in the rate of favorable outcomes received by the unprivileged group compared to the privileged group. A value close to 0 indicates fairness.
    -   *Formula:* `P(favorable_outcome | unprivileged_group) - P(favorable_outcome | privileged_group)`

# Contributing
Contributions are welcome! If you'd like to contribute to this project, please follow these steps:
1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature/your-feature-name`).
3.  Make your changes and commit them (`git commit -m 'Add some feature'`).
4.  Push to the branch (`git push origin feature/your-feature-name`).
5.  Open a Pull Request.

Please ensure your code adheres to good coding practices and includes relevant documentation or comments.

# License
This project is licensed under the MIT License. See the `LICENSE` file for details. (Note: I will need to create a `LICENSE` file or confirm if one should be added based on the project's requirements).
