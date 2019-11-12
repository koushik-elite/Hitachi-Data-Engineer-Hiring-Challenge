**1. How did you approach the data pre-processing, data cleaning and data normalization? Attach the Queries used here.** [10 marks]

I had done data cleaning directly using pandas in python programing.

1, Converting the time to milliseconds on that same day

dt = datetime.datetime.strptime(x, "%I:%M:%S %p")
seconds = dt.second + dt.minute * 60 + dt.hour * 60 * 60

2, Convert all the station string to proper number by removing the string "station$"

x = x.replace("station$", "")

3, calculate the distance between 2 stations using the longitude_source, latitude_source, longitude_destination, latitude_destination

4, fill all empty numeric values with 0 and Category values with None

5, calculate the difference between mean_halt_times_source and mean_halt_times_destination

dataset["halt_times_diff"] = np.abs(dataset["mean_halt_times_source"] - dataset["mean_halt_times_destination"])

6, calculate the delay time for each train by taking the difference between previous train and current train time "current_time"

delay_time = dataset_block["current_time"].diff().values

7, Normalize each column using "StandardScaler" (mean and SD technique) to reduce skewness

8, Convert the "is_weekend" and "target" field numeric 

Target_Volume = {"high": 2, "medium": 1, "low": 0 }
Predict_Volume = {2: "high", 1: "medium", 0: "low" }
is_weekend = {"False": 0 , "True": 1}

8, Finally convert all the category field to One hot encoding and removed the original category fields

**2. How did you approach the problem statement? Explain briefly** [5 Marks]

First i done all the Data preprocessing and then i upplied basic machine learning model to test the data

in second notebook "Hitachi Data Engineer Hiring Challenge.ipynb"
i split the data to train and test with random seed in 80-20 ratio (8:2 train:test) random split
then i used basic machine learning model "LogisticRegression", "DecisionTreeClassifier" and "GaussianNB" to train and validate the data
here "LogisticRegression" with multi_class given better result so i proceed with "LogisticRegression"

in second notebook "Hitachi Data Engineer Hiring Challenge v2.ipynb"
i used StratifiedKFold for data spliting and training and finally produce the mean of the predicted result.

**3.a. Give an example of similar data available on a larger scale and your recommended Hadoop architecture to maintain the data.** 
**3.b. What is your recommended maintenance activity for the architecture mentioned above** [5 Marks]

For maintenance, first the data need to go for all data preprocessing step given above. and appended with original train data and then go for retraining the model.  
