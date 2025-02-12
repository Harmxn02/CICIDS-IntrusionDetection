# CICIDS Intrusion Detection

## Dataset

The CICIDS2017 dataset is a comprehensive dataset for network intrusion detection, created by the Canadian Institute for Cybersecurity. It includes a diverse set of attack scenarios and normal traffic, making it suitable for training and evaluating intrusion detection systems.

The dataset includes various types of attacks such as Brute Force, Heartbleed, Botnet, DoS (Denial of Service), DDoS (Distributed Denial of Service), Web attacks, and Infiltration of the network from inside.

**Dataset**: CIC-IDS2017. (2024, February 1). <https://www.unb.ca/cic/datasets/ids-2017.html>

## Repository contents

1. `main.ipynb`: This Jupyter notebook contains the EDA (exploratory data analysis), preprocessing, model architecture, and model evaluation (for all the data)
1. `main_tuesday.ipynb`: This Jupyter notebook contains the EDA (exploratory data analysis), preprocessing, model architecture, and model evaluation (only for Tuesday's data)
1. `hybrid_model.ipynb`: This Jupyter notebook contains the EDA (exploratory data analysis), preprocessing, model architecture, and model evaluation (for all the data) for a hybrid model explained in this research paper: <https://www.jait.us/articles/2024/JAIT-V15N7-886.pdf>
1. `/data/`: contains the cleaned and encoded datasets, which were exported in the Jupyter notebook
1. `/models/`: contains the trained model which was exported in the Jupyter notebook
1. `requirements.txt`: This file contains the required Python packages to run the Jupyter notebooks

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

#### Classification report 2

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

### All data (Hybrid model)

Here, the model was trained on the CICIDS2017 dataset, using all the data, and a hybrid CNN-GAN model. The architecture is explained in this research paper: <https://www.jait.us/articles/2024/JAIT-V15N7-886.pdf>. The data preprocessing done here are the exact same as the ones done in the `main.ipynb` notebook. The only thing that is different is the model architecture.

The research paper claims their CNN-GAN hybrid model performs better, and that is exactly what I noticed as well. During training I log the epochs and the loss and accuracy for that epoch. Here are those results:

**Regular model**:
Epoch [1/5] - Progress: 100.00% - loss: 2.0223 ; accuracy: 0.7927
Epoch [2/5] - Progress: 100.00% - loss: 2.0092 ; accuracy: 0.8052
Epoch [3/5] - Progress: 100.00% - loss: 2.0026 ; accuracy: 0.8119
Epoch [4/5] - Progress: 100.00% - loss: 2.0022 ; accuracy: 0.8122
Epoch [5/5] - Progress: 100.00% - loss: 2.0020 ; accuracy: 0.8124

**Hybrid model**:
Epoch [1/5] - Progress: 100.00% - Loss: 0.1475 - Accuracy: 0.9282
Epoch [2/5] - Progress: 100.00% - Loss: 0.1140 - Accuracy: 0.9427
Epoch [3/5] - Progress: 100.00% - Loss: 0.1078 - Accuracy: 0.9444
Epoch [4/5] - Progress: 100.00% - Loss: 0.1051 - Accuracy: 0.9452
Epoch [5/5] - Progress: 100.00% - Loss: 0.1032 - Accuracy: 0.9459

This was only for 5 epochs, and the hybrid model already outperforms the regular model. The hybrid model has a higher accuracy and a lower loss. This is a clear indication that the research paper is correct in saying that their hybrid model performs better.

#### Classification report 3

|                            | precision | recall | f1-score | support |
| -------------------------- | --------- | ------ | -------- | ------- |
| BENIGN                     | 1.00      | 0.97   | 0.99     | 454208  |
| Dos Hulk                   | 0.95      | 1.00   | 0.97     | 45782   |
| PortScan                   | 0.90      | 1.00   | 0.95     | 31877   |
| DDoS                       | 1.00      | 1.00   | 1.00     | 25786   |
| DoS GoldenEye              | 0.87      | 1.00   | 0.93     | 2074    |
| FTP-Patator                | 0.94      | 1.00   | 0.97     | 1572    |
| SSH-Patator                | 0.57      | 1.00   | 0.73     | 1128    |
| DoS slowloris              | 0.72      | 0.99   | 0.83     | 1166    |
| DoS Slowhttptest           | 0.85      | 0.99   | 0.91     | 1109    |
| Bot                        | 0.10      | 0.99   | 0.19     | 441     |
| Web Attack � Brute Force   | 0.27      | 0.49   | 0.34     | 301     |
| Web Attack � XSS           | 0.15      | 0.79   | 0.25     | 119     |
| Infiltration               | 0.14      | 0.71   | 0.23     | 7       |
| Web Attack � Sql Injection | 0.02      | 0.50   | 0.03     | 4       |
| Heartbleed                 | 1.00      | 1.00   | 1.00     | 2       |
|                            |           |        |          |         |
| accuracy                   |           |        | 0.98     | 565576  |
| macro avg                  | 0.63      | 0.90   | 0.69     | 565576  |
| weighted avg               | 0.99      | 0.98   | 0.98     | 565576  |

The hybrid model performs better than the regular model, with an accuracy of **97.75%** and an F1 score of **98.12%**. The hybrid model performs better on all attack types, except for **Bot**, **Web Attack � Brute Force**, **Web Attack � XSS**, **Infiltration**, **Web Attack � SQL Injection**, and **Heartbleed**. This is, again, likely due to the low number of samples for these attack types.

I think if the hybrid model was trained for more epochs, it would perform even better. However, I only trained it for 5 epochs.
