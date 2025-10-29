Phishing Email Detection Project: Data Generation Module

📝 Overview

This repository contains the foundation for a Phishing Email Detection System using Natural Language Processing (NLP) and a Logistic Regression classifier.

The script documented here, generate_sample_dataset.py, is responsible for creating a small, labeled sample dataset and generating corresponding metadata to ensure data provenance and reproducibility for the entire project.

🚀 Quickstart: Generating the Dataset

To create the initial data files (phishing_emails.csv and dataset_metadata.json), run the following script:

python generate_sample_dataset.py


Prerequisites

You need Python installed, along with the necessary libraries (which can typically be installed via a requirements.txt file):

pip install pandas


📂 Files Generated

Running the script creates two crucial files:

File Name

Description

Purpose

phishing_emails.csv

The raw, labeled dataset.

Used by the main training script (phishing_nlp_detection.py) as input.

dataset_metadata.json

Documentation file.

Provides data provenance (who, when, how many samples) and defines the label map.

💻 generate_sample_dataset.py Source Code

This script defines the synthetic samples and exports them along with structured metadata.

import pandas as pd
from datetime import datetime
import json

# Define initial samples: (text, label)
# Label 1: Phishing, Label 0: Legitimate
samples = [
    ("Your account has been locked due to suspicious activity...", 1),
    ("Dear user, update your payment method to avoid service interruption.", 1),
    ("You have won $500,000! Reply with your bank details to claim your prize.", 1),
    ("Team meeting tomorrow at 10 AM", 0),
    ("Please find attached the monthly invoice", 0)
]

df = pd.DataFrame(samples, columns=['text','label'])
csv_path = 'phishing_emails.csv'
df.to_csv(csv_path, index=False)

# Metadata generation for provenance
metadata = {
    # Replace the placeholder with the actual creator's name/roll number
    "generated_by": "<Your Name / Roll No.>",
    "generated_at": datetime.utcnow().isoformat() + "Z",
    "num_samples": len(df),
    "label_map": {"1":"phishing","0":"legitimate"}
}
with open('dataset_metadata.json','w') as f:
    json.dump(metadata, f, indent=2)

print(f"Saved {csv_path} and dataset_metadata.json")


🛠️ Data Provenance (dataset_metadata.json Example)

The generated JSON file clearly defines the data structure for reproducibility.

{
  "generated_by": "Student Roll No: XXXXXX",
  "generated_at": "2025-10-29T08:52:15.123456Z",
  "num_samples": 5,
  "label_map": {
    "1": "phishing",
    "0": "legitimate"
  }
}


🎯 Next Steps (Full Project Pipeline)

This module feeds into the larger Phishing Detection System. The typical subsequent steps are:

Preprocessing: Clean the text from phishing_emails.csv (remove URLs, stop words, etc.).

Feature Extraction: Use TF-IDF to vectorize the cleaned text.

Model Training: Train the Logistic Regression classifier on the TF-IDF vectors using the labels.

Testing: Evaluate the model's performance using unit tests and metrics.
