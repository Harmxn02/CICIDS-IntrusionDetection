# NSL-KDD Intrusion Detection

## Dataset

The CICIDS2017 dataset is a comprehensive dataset for network intrusion detection, created by the Canadian Institute for Cybersecurity. It includes a diverse set of attack scenarios and normal traffic, making it suitable for training and evaluating intrusion detection systems.

The dataset includes various types of attacks such as Brute Force, Heartbleed, Botnet, DoS (Denial of Service), DDoS (Distributed Denial of Service), Web attacks, and Infiltration of the network from inside.

**Dataset**: CIC-IDS2017. (2024, February 1). <https://www.unb.ca/cic/datasets/ids-2017.html>

## Repository contents

1. `main.ipynb`: This Jupyter notebook contains the EDA (exploratory data analysis), preprocessing, model architecture, and model evaluation
1. `/data/`: contains the cleaned and encoded datasets, which were exported in the Jupyter notebook
1. `/models/`: contains the trained model which was exported in the Jupyter notebook

## Model performance

The model was trained on the CICIDS2017 dataset, however only on the data from Tuesdat

### Classification report

|              | precision | recall | f1-score | support |
| ------------ | --------- | ------ | -------- | ------- |
| BENIGN       | 1.00      | 1.00   | 1.00     | 86310   |
| FTP-Patator  | 0.97      | 1.00   | 0.99     | 1587    |
| SSH-Patator  | 0.86      | 0.99   | 0.92     | 1232    |
|              |           |        |          |         |
| accuracy     |           |        | 1.00     | 89129   |
| macro avg    | 0.95      | 0.99   | 0.97     | 89129   |
| weighted avg | 1.00      | 1.00   | 1.00     | 89129   |

The model performs pretty well, with an accuracy of **99.72%**. If we look at the performance per attack type, there are some outliers:

- **SSH-Patator**: this attack type has a lower precision of **86%**, which means that the model is not as good at identifying this attack type

- **FTP-Patator**: this attack type has a lower recall of **97%**, which means that the model is not as good at identifying all instances of this attack type
