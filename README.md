# Capstone_Project

**The Problem Area:**  Energy consumption/Energy Load Prediction

The focus of my project is on energy consumption and load prediction, specifically in the context of residential electric vehicle (EV) charging in apartment buildings. One of the primary challenges in this domain is optimizing energy usage, balancing the demand for EV charging with other household electricity needs, and predicting the overall energy load on the building. Additionally, understanding the impact of external factors such as weather conditions and local traffic density on energy consumption during charging sessions is crucial for efficient resource allocation and infrastructure planning.

**The User:** The primary users experiencing the challenges in this scenario are residents of the apartment buildings, particularly those who own or use electric vehicles. These users would benefit from the outcomes of the project by having a more reliable and efficient EV charging infrastructure. Predictive models can help users plan their charging sessions, optimize energy consumption, and potentially reduce costs. Additionally, property managers and energy providers can benefit from insights into the overall energy load patterns, enabling them to make informed decisions about infrastructure upgrades and energy distribution.

**The Big Idea:** Machine learning can play a pivotal role in addressing the challenges of energy consumption and load prediction in residential EV charging. By leveraging the provided datasets, including EV charging reports, hourly charging loads, idle capacity, weather data, and traffic density, predictive models can be developed. Previous approaches might include time-series forecasting techniques, regression models, and possibly neural networks to capture the complex relationships between charging patterns and various influencing factors. The goal is to create models that can accurately predict future energy loads based on historical charging sessions, weather conditions, and traffic density, allowing for proactive energy management.

**The Impact:** The anticipated impact of this project is twofold. Firstly, at a societal level, optimizing energy consumption in residential EV charging can contribute to overall energy efficiency and sustainability. This has the potential to reduce the carbon footprint associated with electricity generation. Secondly, from a business perspective, property managers and energy providers stand to gain by implementing more efficient and predictive energy management strategies. The quantifiable impact could include reduced energy costs, optimized infrastructure investments, and potentially a more reliable and convenient charging experience for EV users. The scale of the impact could be measured in terms of energy savings, cost reductions, and improvements in overall energy grid efficiency.

### Description of a Dataset

Data have been collected from a large housing cooperative in Norway, with 1,113 apartments and 2,321 residents. A new infrastructure for EV charging was installed from December 2018. From December 2018 to January 2020, charging sessions were registered by 97 user IDs; 82 of these IDs appeared to be still active at the end of the period. In the data provided with this article, Central European Time (CET) zone is used

**Dataset 1: EV charging reports**

The CSV file “Dataset 1” describes 6,878 individual charging sessions, registered by 97 user
IDs from December 2018 to January 2020. The charging reports include plug-in time, plug-out
time and charged energy per charging session. Each charging session is connected to a user
ID, charger ID and address.

**Dataset 2: Hourly EV charging loads and idle capacity, for all sessions and users individually**

The CSV file “Dataset 2” describes EV charging loads and non-charging idle capacity for each
user and all EV charging sessions individually. Charging power 3.6 kW or 7.2 kW is assumed, with immediate charging after plug-in. The non-charging idle time reflects the flexibility potential for the charging session. Synthetic idle capacity is the energy load that could potentially have been charged during the idle times.

**Dataset 3 and 4: Hourly EV charging loads and idle capacity, aggregated for private or shared CPs**

The CSV files “Dataset 3a” and “Dataset 3b” describe EV charging loads and idle capacity,
aggregated for users with private (3a) or shared (3b) CPs. Charging power 3.6 kW or 7.2 kW
is assumed, with immediate charging after plug-in.

**Dataset 5: Hourly smart meter data from garage Bl2**

The CSV file describes hourly smart meter data from garage Bl2, with aggregated electricity use each hour. The EVs were parked in 24 locations, whereof 22 locations have an AMS-meter measuring aggregated EV-charging at that location, with hourly resolution AMS-measurements from a main garage, where 33% of the charging sessions took place (2,243 charging sessions).

**Dataset 6: Local traffic density**

Local hourly traffic density in 5 nearby traffic locations. The data includes an hourly count of vehicles shorter than 5.6 meter, from December 2018 to January 2020.

**Dataset 7: Weather Data**

Local Weather Data of Trondheim, Norway.The data includes weather features like temperature, rainfall etc from December 2018 to January 2020.

# Getting familiar with capstone project.

***What is Energy consumption/Energy Load Prediction***

Energy consumption or energy load prediction refers to the use of predictive models and algorithms to estimate the future energy consumption patterns of a system or a specific device. In the context of residential electric vehicle (EV) charging, energy load prediction involves forecasting the amount of electricity that will be consumed during charging sessions over a given period.

***The main goals of energy load prediction in the context of EV charging are:***
1.	Optimizing Resource Allocation: Predicting when and how much energy will be consumed allows for better planning and allocation of resources, preventing overloads and ensuring the availability of sufficient energy when needed.
2.	Infrastructure Planning: Property managers and energy providers can use predictions to plan and optimize the infrastructure for EV charging, ensuring that it meets the growing demand without unnecessary costs.
3.	User Convenience: Predictive models enable users to plan their charging sessions more effectively, taking advantage of times with lower energy costs or higher renewable energy availability.
4.	Energy Efficiency: By anticipating energy demands, it becomes possible to implement strategies to promote energy efficiency and reduce overall energy consumption.

## Exploratory Data Analysis (EDA):

Basic EDA, getting familiar with data. 

Clening, dealing with missing values and duplicates.

Merging datasets. This step was actually challenging. As i was merging 7 datasets togheter and by merging each of them I was trying fill NaN values, as some columns was identical but contained more values.

Identifing Target variable and feature variables.

# Feature Engineering and Further Cleaning Steps to work on

#### 1. Feature Engineering
- Extract datetime features

df['hour_of_day'] = df['Start_plugin'].dt.hour
df['day_of_week'] = df['Start_plugin'].dt.dayofweek
df['month'] = df['Start_plugin'].dt.month

#### 2. Encoding Categorical Variables
- Example: One-hot encoding for 'User_type' column

df = pd.get_dummies(df, columns=['User_type'], prefix='user_type')

### 3. Correlation Analysis
- Explore the correlation matrix

correlation_matrix = df.corr()

#### 4. Feature Scaling (if needed)
- Standardize or normalize numerical features

#### 5. Handling Outliers
- Identify and handle outliers in numerical features

#### 6. Check for Imbalanced Classes (if Classification)
- Explore the distribution of classes and handle imbalances

#### 7. Check for Skewed Target Variable (if Regression)
- Address skewness if necessary using transformations

#### 8. Other Steps Based on Data Characteristics
- Any other preprocessing steps based on insights from EDA

#### Update X and y after adding new features or encoding
X = df.drop(['El_kWh'], axis=1)
y = df['El_kWh']

# Baseline Models:
## Mean Baseline model
- I Started with basic one. And will use it as an example to compare RMSE value to any other new models.
## Linear Regression model / Scaled version
- With regression model need to choose right scaling method, that will be better for my dataset. Otherwise it was no minor difference betwen Scaled and not scaled regression models.
## Decision Tree Regressor:
Worse than Linear regression
## Linear regression with PCA
- BEtter performing than others. First of all as I havent drop any higly correlated features, PCA helps here.
- Second, I used Cross Validation and Plotted n_components to find best number of PCA components to use.
