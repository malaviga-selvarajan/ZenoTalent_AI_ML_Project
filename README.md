# Payroll Anomaly Detection

### Introduction
Built an unsupervised machine learning system to detect payroll fraud in NYC employee data, specifically targeting salary manipulation and fake overtime claims without requiring labeled training data.

## Project Summary

### Tasks Completed
1. Data Loading & Exploration

Loaded 50,000 records from NYC Open Data API
Explored dataset structure with 17 columns including base_salary, ot_hours, title_description
Verified data quality and checked for missing values

2. Feature Engineering

Created comparison features: salary vs title average, salary vs agency average
Built overtime ratios: OT pay/base salary, OT hours/full-time hours
Calculated pay discrepancies between base and actual gross paid

3. Anomaly Detection (Unsupervised Learning)

Algorithm: Isolation Forest (contamination=0.05)
Salary Detection: Flags unusual compensation patterns by job title and agency
Overtime Detection: Identifies excessive overtime hours and pay
Combined Detection: Uses all features with one-hot encoding for categorical variables

4. Concept Drift Handling

Loads new data batch (10,000 records with offset)
Compares mean and standard deviation shifts
Triggers retraining alert if >15% mean shift or >25% std shift detected

5. Pipeline Implementation

Batch Pipeline: Processes entire dataset at once, generates top anomalies
Real-Time Pipeline: process_realtime_record() function evaluates single transactions instantly

6. Visualization

Scatter plot showing salary anomalies by job title
Histogram comparing normal vs anomalous salary distribution
Overtime hours vs pay scatter plot with anomaly highlighting

### Algorithm Selection Rationale

Isolation Forest chosen because:
- Works without labeled data (unsupervised)
- Efficient for high-dimensional data
- Isolates anomalies based on how easily they separate from normal patterns
- Handles both numeric and categorical features after preprocessing

### Evaluation Strategy (No Labels):
- Count anomalies detected (5% contamination rate)
- Manual review of top 5 suspicious cases for salary and overtime
- Compare results across three detection approaches (salary-only, overtime-only, combined)
- Visual inspection through interactive plots

### Deployment Plan
- Schedule daily batch processing for all payroll records
- Deploy real-time API endpoint for new transaction validation
- Set up weekly drift monitoring to check model validity
- Retrain models monthly or when drift threshold exceeded
- Human review queue for flagged anomalies above threshold

### Conclusion
Successfully implemented a complete anomaly detection system meeting all requirements: uses unsupervised learning (Isolation Forest), detects both salary and overtime fraud, handles concept drift monitoring, and provides both batch and real-time processing capabilities. The system identified anomalies without requiring labeled training data and can adapt to changing payroll patterns over time.

### References:

I had collected data and explored websites for the project. Highlighting the references below:

https://community.sap.com/t5/human-capital-management-blog-posts-by-sap/ai-based-anomaly-monitoring-using-sap-payroll-control-center/ba-p/13965841

https://www.next.gr/ai/ai-in-finance/payroll-anomaly-detection-with-ml

https://www.neeyamo.com/blog/impact-machine-learning-payroll-fraud-detection

#### Dataset link

https://data.cityofnewyork.us/City-Government/Citywide-Payroll-Data-Fiscal-Year-/k397-673e/about_data
