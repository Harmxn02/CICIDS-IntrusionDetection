# CICIDS Intrusion Detection

## Dataset

The CICIDS2017 dataset is a comprehensive dataset for network intrusion detection, created by the Canadian Institute for Cybersecurity. It includes a diverse set of attack scenarios and normal traffic, making it suitable for training and evaluating intrusion detection systems.

The dataset includes various types of attacks such as Brute Force, Heartbleed, Botnet, DoS (Denial of Service), DDoS (Distributed Denial of Service), Web attacks, and Infiltration of the network from inside.

**Dataset**: CIC-IDS2017. (2024, February 1). <https://www.unb.ca/cic/datasets/ids-2017.html>

## Repository contents

1. `main.ipynb`: This Jupyter notebook contains the EDA (exploratory data analysis), preprocessing, model architecture, and model evaluation (for all the data)
1. `main_tuesday.ipynb`: This Jupyter notebook contains the EDA (exploratory data analysis), preprocessing, model architecture, and model evaluation (only for Tuesday's data)
1. `/data/`: contains the cleaned and encoded datasets, which were exported in the Jupyter notebook
1. `/models/`: contains the trained model which was exported in the Jupyter notebook

## Model performance

### Tuesday's data

Here, the model was trained on the CICIDS2017 dataset, however only on the data from Tuesday

#### Classification report

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

### All data

Here, the model was trained on the CICIDS2017 dataset, using all the data

#### Classification report 2: TO-DO

|                            | precision | recall | f1-score | support |
| -------------------------- | --------- | ------ | -------- | ------- |
| BENIGN                     | 0.99      | 0.96   | 0.98     | 454208  |
| Dos Hulk                   | 1.00      | 0.71   | 0.83     | 45782   |
| PortScan                   | 0.83      | 1.00   | 0.91     | 31877   |
| DDoS                       | 0.75      | 1.00   | 0.86     | 25786   |
| DoS GoldenEye              | 0.70      | 1.00   | 0.82     | 2074    |
| FTP-Patator                | 0.98      | 1.00   | 0.99     | 1572    |
| SSH-Patator                | 0.94      | 0.48   | 0.64     | 1128    |
| DoS slowloris              | 0.78      | 0.87   | 0.82     | 1166    |
| DoS Slowhttptest           | 0.84      | 0.68   | 0.75     | 1109    |
| Bot                        | 0.08      | 0.99   | 0.14     | 441     |
| Web Attack � Brute Force   | 0.00      | 0.00   | 0.00     | 301     |
| Web Attack � XSS           | 0.05      | 0.97   | 0.10     | 119     |
| Infiltration               | 0.04      | 0.71   | 0.07     | 7       |
| Web Attack � Sql Injection | 0.00      | 0.00   | 0.00     | 4       |
| Heartbleed                 | 0.07      | 1.00   | 0.12     | 2       |
|                            |           |        |          |         |
| accuracy                   |           |        | 0.95     | 565576  |
| macro avg                  | 0.54      | 0.76   | 0.54     | 565576  |
| weighted avg               | 0.96      | 0.95   | 0.95     | 565576  |

The model performs okay on most attack types with an accuracy of **94.52%** and an F1 score of **95.09%**. However, it performs horribly on a few attack types, namely: **Bot**, **Web Attack � Brute Force**, **Web Attack � XSS**, **Infiltration**, **Web Attack � SQL Injection**, and **Heartbleed**. This is likely due to the low number of samples for these attack types.
