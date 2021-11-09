# Orioles Attendance Prediction – Model Card

### Basic Information

* **Persons involved in developing model**: Yasir Mohammad - `yasir@gwu.edu`
* **Model date**: November, 2021
* **Model version**: 1.0
* **License**: MIT License
* **Model implementation code**:
  * **Python Model**: [Credit_Line_Increase_Project_Python_Model.ipynb](https://github.com/yasirbm/DNSC6301---Analytics-Edge/blob/main/Python_Model/Credit_Line_Increase_Project_Python_Model.ipynb)

### Intended Use
* **Primary intended uses**: This model is intended to predict attendance for 2022 home games played by the Baltimore Orioles

### Data Source & Data Dictionary

* ![](images/model_variables.jpg)
* **How data was split into training and test data**: 80% training, 20% test

### Model Details
* **Columns used as inputs in the final model**: 
![image](https://user-images.githubusercontent.com/89418186/131267179-aa1cfb80-98b6-454e-9790-3b382e6d6368.png)
*	**Columns used as targets in the final model**: ATTENDANCE
* **Type of Model**: Multiple Regression
*	**Software used to train the Model**: Python v3.8.8
*	**Metrics used to evaluate the model and final figures**:
  * **R Squared**: 0.923
  * **Adjusted R Squared**: 0.919

### Data Visualizations
* **Correlation Heatmap**:
![](images/corr_heatmap.png)

* **Attendance by Year**:
![](images/Attendance by year.png)
