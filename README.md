# dataset-for-phishing-emails-using-Natural-Language-Processing-NLP-.
# generate_sample_dataset.py
import pandas as pd
from datetime import datetime
import json

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

metadata = {
    "generated_by": "<Teammate C name>",
    "generated_at": datetime.utcnow().isoformat() + "Z",
    "num_samples": len(df),
    "label_map": {"1":"phishing","0":"legitimate"}
}
with open('dataset_metadata.json','w') as f:
    json.dump(metadata, f, indent=2)

print(f"Saved {csv_path} and dataset_metadata.json")
