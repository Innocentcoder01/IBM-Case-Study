# Case Study: AI-Driven Detection of Malicious DGA Domains

This repository contains the final case study report, "AI-Driven Security: Detecting Malware Command-and-Control (C2) with Machine Learning using Java and Weka," submitted for IBM.

The full, step-by-step report with all screenshots and analysis is available by *downloading the PDF file in this repository.*

---

## 1. 🎯 Study Aim & Introduction

### The Problem
In modern cybersecurity, *Domain Generation Algorithms (DGAs)* are a primary technique used by malware to evade detection. Instead of using a static, hard-coded domain (e.g., malware-control.com)—which can be easily blocked—malware uses a DGA to generate thousands of new, pseudo-random domains every day (e.g., ax8fj-random-site-29.com). The attacker only needs to register one of these domains to establish a *Command-and-Control (C2)* channel with their infected machines, making traditional blacklisting ineffective.

### The Solution
This project builds a *Security Intelligence tool* using supervised machine learning to solve this problem. The tool is trained to act as a classifier, analyzing the linguistic and statistical properties of a domain name to predict, with high accuracy, whether it is **benign** (legitimate) or **dga** (malicious).

---

## 2. 🛠 Methodology & Tools

This case study follows the complete data science workflow, from data collection to model evaluation.

### Key Tools
* *Language:* *Java* (JDK)
* *Data Mining Suite:* *Weka 3.8*
* *Classification Algorithm:* *Random Forest* (weka.classifiers.trees.RandomForest)

### Step 1: Feature Engineering (Java)
The model cannot understand text. A custom Java program (FeatureExtractor.java) was written to convert raw domain names into numerical features.

* *Dataset:* A balanced dataset of 50,000 domains was created (25,000 benign, 25,000 DGA).
* *Features Calculated:*
    1.  **domain_length**: The total number of characters in the domain.
    2.  **digit_ratio**: The percentage of characters that are numbers (0-9).
    3.  **shannon_entropy**: The most important feature. This is a mathematical score of randomness. A real word like google has *low entropy*, while a DGA domain like k2j8d9s0f has *high entropy*.

### Step 2: Data Visualization (Weka)
The resulting .arff file was loaded into the Weka Explorer. A scatter plot visualization immediately confirmed our hypothesis:
* *Benign domains* (blue) clustered at a *low entropy* value.
* *DGA domains* (red) clustered at a *high entropy* value.
This clear separation proved that a machine learning model could be trained to find this pattern.

### Step 3: Model Training (Weka)
A *Random Forest* classifier was chosen. This is a powerful ensemble model that builds hundreds of "decision trees" and combines their votes to make a final prediction.

The model was trained and tested using *10-fold cross-validation*, a robust method to ensure the results were accurate and not due to chance.

---

## 3. 📊 Results & Analysis

The 10-fold cross-validation test on the 50,000-domain dataset yielded the following results:

* *Overall Model Accuracy:* *84.202%*
* *Time to build model:* 14.15 seconds

### Confusion Matrix
This table shows the model's performance in detail:

| | Classified as benign | Classified as dga |
| :--- | :---: | :---: |
| **Actual benign** | *20,145* (True Negative) | *4,855* (False Positive) |
| **Actual dga** | *3,044* (False Negative) | *21,956* (True Positive) |

### Analysis
* *High False Negatives:* The model had *3,044 False Negatives*. This is the most critical error for a security tool, as it means 3,044 malicious domains were incorrectly labeled as "safe."
* *High False Positives:* The model had *4,855 False Positives*, which would create a high volume of false alarms for a security analyst.

## 4. 🏁 Conclusion

The case study was a success in *proving the concept* that machine learning can be used to detect DGA domains based on linguistic features. An accuracy of *84.2%* is a strong result for a model built on only three basic features.

However, the high false-negative and false-positive rates indicate that this model, in its current form, is not reliable enough for a production environment. To improve this tool, future work would need to include more advanced **feature engineering**, such as n-gram analysis (analyzing common letter combinations) and vowel-consonant ratios, to better distinguish the subtle patterns of more sophisticated DGAs.

---
> *To see the full, step-by-step process with all screenshots and settings, please download and read the attached PDF report.*
