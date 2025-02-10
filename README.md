# NSL-KDD Intrusion Detection

## Dataset

The CICIDS2017 dataset is a comprehensive dataset for network intrusion detection, created by the Canadian Institute for Cybersecurity. It includes a diverse set of attack scenarios and normal traffic, making it suitable for training and evaluating intrusion detection systems.

The dataset includes various types of attacks such as Brute Force, Heartbleed, Botnet, DoS (Denial of Service), DDoS (Distributed Denial of Service), Web attacks, and Infiltration of the network from inside.

**Dataset**: CIC-IDS2017. (year, date). <https://www.unb.ca/cic/datasets/ids-2017.html>

## Repository contents

1. `main.ipynb`: This Jupyter notebook contains the EDA (exploratory data analysis), preprocessing, model architecture, and model evaluation
1. `/data/`: contains the cleaned and encoded datasets, which were exported in the Jupyter notebook
1. `/models/`: contains the trained model which was exported in the Jupyter notebook

## Model performance

### Classification report

|              | precision | recall | f1-score | support |
| ------------ | --------- | ------ | -------- | ------- |
| normal       | 1.00      | 0.95   | 0.97     | 12992   |
| neptune      | 1.00      | 1.00   | 1.00     | 4043    |
| ipsweep      | 0.97      | 0.97   | 0.97     | 706     |
| satan        | 0.61      | 0.98   | 0.75     | 711     |
| smurf        | 0.93      | 1.00   | 0.96     | 511     |
| portsweep    | 0.97      | 1.00   | 0.98     | 501     |
| nmap         | 0.88      | 0.99   | 0.93     | 312     |
| back         | 0.88      | 1.00   | 0.94     | 179     |
| teardrop     | 1.00      | 1.00   | 1.00     | 166     |
| warezclient  | 0.48      | 0.99   | 0.65     | 111     |
|              |           |        |          |         |
| accuracy     |           |        | 0.96     | 20232   |
| macro avg    | 0.87      | 0.99   | 0.92     | 20232   |
| weighted avg | 0.98      | 0.96   | 0.97     | 20232   |

The model performs [performance], with an accuracy of **XX%**. If we look at the performance per attack type, there are some outliers:

- **XX**: finding

- **XX**: finding
