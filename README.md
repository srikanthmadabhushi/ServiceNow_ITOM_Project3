# ServiceNow_ITOM_Project4
# ServiceNow ITOM Project 4 – Federated AIOps (PDI Simulation)

## 🧭 Objective  
Simulate an AI-driven anomaly detection and auto-remediation workflow in ServiceNow (Yokohama PDI), leveraging machine learning logic and Flow Designer to detect high-CPU or memory anomalies across multiple “regions” (Region A & Region B), apply a federated global policy, and automatically create incidents for remediation.

## 📋 Modules & Technologies  
- ServiceNow – Yokohama PDI  
- Predictive Intelligence (Classification model)  
- Flow Designer – Auto-remediation logic  
- Tables: Metric Event, Incident  
- Concepts: Regions, Federated model policy, Auto-Remediation  
- Skills: AI + ServiceNow + ITOM + Agile automation  

## 🏗 Architecture  
Insert your flowchart image here (`/Screenshots/flowchart.png`)  
**Description:**  
1. Metric Event is created (CI, region, metric_name, metric_value)  
2. Model evaluates whether `is_anomaly = true`  
3. If true → Flow Designer triggers incident creation + work note + notification  
4. Federated concept demonstrated via separate region data feeding into a global policy  
5. Dashboard displays anomaly counts, auto-remediation incidents, regional splits  

## ✅ Step-by-Step Build  
### 1. Table Setup  
- Created custom table **Metric Event** with fields:  
  `ci` (reference to cmdb_ci), `region`, `metric_name`, `metric_value`, `timestamp`, `is_anomaly` (True/False)  
- Inserted ~20 sample records (10 anomalies, 10 normal) across Regions A & B  

### 2. Solution Definition (Classification)  
- Created Solution Definition:  
  - Name: *Anomaly Predictor – Metric Events*  
  - Table: Metric Event  
  - Field to predict: `is_anomaly`  
  - Input features: `metric_value`, `region`, `metric_name`, `ci`  
- Saved and verified definition  

### 3. Model Training & Publishing  
- (If available) Generated and trained the model → Accuracy: __%  
- Published model for use  

### 4. Flow Designer (Auto-Remediation)  
- Flow Name: *AIOps – Auto-Remediate Predicted Anomalies*  
- Trigger: Record Insert on Metric Event  
- If condition: `prediction = true` (or `metric_value ≥ 90` fallback)  
- Actions: Create Incident (short desc: “Predicted Anomaly on ${ci} (${metric_value}%)”), add Work Notes, send Notification  
- Flow Activated  

### 5. Testing & Results  
- **Test Case A:** Region A → CPU 95 → Incident auto-created ✅  
- **Test Case B:** Region B → CPU 75 → No incident ✅  
- Screenshots:  
  - Table seed data  
  - Model/training results  
  - Flow Designer configuration  
  - Incident record created  
  - Dashboard showing anomalies by region  

### 6. Future Enhancements  
- Integrate real orchestration to restart services or scale resources  
- Add learning feedback loop: user confirmation updates model training set  
- Expand to additional metrics (memory, disk, network) and more regions  
- Integrate with Snowflake or Jira for event ingestion and ticket creation
