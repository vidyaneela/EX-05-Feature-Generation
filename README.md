## EX-05-Feature-Generation
# AIM
To read the given data and perform Feature Generation process and save the data to a file.

# Explanation
Feature Generation (also known as feature construction, feature extraction or feature engineering) is the process of transforming features into new features that better relate to the target.

It includes two process:

Feature Encoding Feature Scaling

## FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.

2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.

3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.

4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

## FEATURE SCALING:
1. Standard Scaler
It is also called Z-score normalization. It calculates the z-score of each value and replaces the value with the calculated Z-score. The features are then rescaled with x̄ =0 and σ=1

2. MinMaxScaler
It is also referred to as Normalization. The features are scaled between 0 and 1. Here, the mean value remains same as in Standardization, that is, 0.

3. Maximum absolute scaling
Maximum absolute scaling scales the data to its maximum value; that is, it divides every observation by the maximum value of the variable.The result of the preceding transformation is a distribution in which the values vary approximately within the range of -1 to 1.

4. RobustScaler
RobustScaler transforms the feature vector by subtracting the median and then dividing by the interquartile range (75% value — 25% value).

# ALGORITHM
STEP 1
Read the given Data

STEP 2
Clean the Data Set using Data Cleaning Process

STEP 3
Apply Feature Generation techniques to all the feature of the data set

STEP 4
Save the data to the file

1.FEATURE GENERATION FOR Data.csv
## CODE FOR FEATURE ENCODING AND FEATURE SCALING:
```
import pandas as pd
df=pd.read_csv("data.csv")
df
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
temp=["Cold","Warm","Hot","Very Hot"]
enc=OrdinalEncoder(categories=[temp])
df["Ord_1"]=enc.fit_transform(df[["Ord_1"]])
df
education=["High School","Diploma","Bachelors","Masters","PhD"]
ed=OrdinalEncoder(categories=[education])
df["Ord_2"]=ed.fit_transform(df[["Ord_2"]])
df
pip install category_encoders
from category_encoders import BinaryEncoder
be=BinaryEncoder()
be.fit_transform(df["bin_1"])
df["bin_1"]=be.fit_transform(df[["bin_1"]])
df
be1=BinaryEncoder()
be1.fit_transform(df["bin_2"])
df["bin_2"]=be1.fit_transform(df[["bin_2"]])
df
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse=False)
ohe.fit_transform(df[["City"]])
from category_encoders import TargetEncoder
te=TargetEncoder()
te.fit_transform(X=df['Ord_1'],y=df["Target"])
le=LabelEncoder()
df["City"]=le.fit_transform(df[["City"]])
df

from sklearn.preprocessing import StandardScaler
sc=StandardScaler()
df1=pd.DataFrame(sc.fit_transform(df),columns=['id','bin_1','bin_2','City','Ord_1','Ord_2','Target'])
df1

from sklearn.preprocessing import MaxAbsScaler
mas=MaxAbsScaler()
df2=pd.DataFrame(mas.fit_transform(df),columns=['id','bin_1','bin_2','City','Ord_1','Ord_2','Target'])
df2

from sklearn.preprocessing import MinMaxScaler
mms=MinMaxScaler()
df3=pd.DataFrame(mms.fit_transform(df),columns=['id','bin_1','bin_2','City','Ord_1','Ord_2','Target'])
df3

from sklearn.preprocessing import RobustScaler
rs=RobustScaler()
df4=pd.DataFrame(rs.fit_transform(df),columns=['id','bin_1','bin_2','City','Ord_1','Ord_2','Target'])
df4
```
# OUTPUT:
## Given DataFrame:
![166728059-2bdba86d-9abb-4a6c-a12c-90bc6d436ae2](https://user-images.githubusercontent.com/94169318/167535075-4bfd1901-3205-4443-a48f-25b591212309.png)

## Feature encoding using Ordinal Encoder:
![166728108-2831a415-36d5-4f1d-a1bb-25f381983cc5](https://user-images.githubusercontent.com/94169318/167535151-79710200-9ee9-4046-9236-10bd91b4abf1.png)
![166728173-343d68df-a199-4b7f-8cef-e3129caa9974](https://user-images.githubusercontent.com/94169318/167535175-8085193d-ae71-4cb5-b0e8-ffaea4125bce.png)

## Feature encoding using Binary Encoder:
![166728205-284d6f7a-2287-4850-aa6e-8e7a73c6d673](https://user-images.githubusercontent.com/94169318/167535212-2f97389b-44c6-4178-9b20-50e51cae1441.png)
![166728236-5b8c2397-0542-471e-9e41-6c96bc6a5bc8](https://user-images.githubusercontent.com/94169318/167535250-769e47ab-8e88-4985-a3dc-23c36d6ea64f.png)
![166728262-64f9bbfd-cc16-4ddc-80f2-02641c89b5e8](https://user-images.githubusercontent.com/94169318/167535283-95949d9f-7fbd-45a0-b581-6ca5e1afea49.png)
![166728364-711ea583-571e-4de4-a7a5-3063c575db65](https://user-images.githubusercontent.com/94169318/167535303-ff2d1a45-0cfc-49af-941a-cd9720690b1b.png)

## Feature encoding using One Hot Encoder:
![166728442-661f0bf7-a8e8-4cb4-a25b-acda2e021b15](https://user-images.githubusercontent.com/94169318/167535353-4fe2310c-4a99-444d-ab66-a2e4ca4fab7c.png)

## Feature encoding using Target Encoder:
![166728475-c75d0e77-7185-4178-abf4-a3823be2647c](https://user-images.githubusercontent.com/94169318/167535391-22d42ed3-df82-4abd-8a71-6b6cbc5cb7c1.png)

## Feature encoding using Label Encoder:
![166728513-50c0bda5-db36-4ad5-ba8f-f3d9375e5bbe](https://user-images.githubusercontent.com/94169318/167535427-52e7169d-176c-4516-84ca-90bd8f53ec3b.png)

## Feature scaling using Standard Scaler:
![166728541-400ff2bc-2c7b-4328-ac3d-68e1da4af6da](https://user-images.githubusercontent.com/94169318/167535463-6744b6b5-3e74-4f21-8c0f-b0b0733bf140.png)

## Feature scaling using MaxAbs Scaler:
![166728573-5b9857fb-1563-43e5-a698-ff92598e509a](https://user-images.githubusercontent.com/94169318/167535541-20ea5766-2e18-4c84-8211-468e8e92fe86.png)

## Feature scaling using MinMax Scaler:
![166728610-d98d7b31-06a9-4be7-9603-cfaf1bb378d3](https://user-images.githubusercontent.com/94169318/167535579-1fde21f6-ed58-493c-a399-cb6a612d5ba0.png)

## Feature scaling using Robust Scaler:
![166728635-fb6eac58-da5a-4d8f-8f88-64abfa3696e6](https://user-images.githubusercontent.com/94169318/167535608-c31c5f58-6ae7-48e5-9e90-2555aae9b3e0.png)

# 2.FEATURE GENERATION FOR Encoding.csv
## CODE FOR FEATURE ENCODING AND FEATURE SCALING:
```
import pandas as pd
df=pd.read_csv("Encoding Data.csv")
df
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
temp=["Cold","Warm","Hot"]
enc=OrdinalEncoder(categories=[temp])
df["ord_2"]=enc.fit_transform(df[["ord_2"]])
df
from category_encoders import BinaryEncoder
be=BinaryEncoder()
df['bin_1']=be.fit_transform(df[['bin_1']])
df
be1=BinaryEncoder()
df['bin_2']=be1.fit_transform(df[['bin_2']])
df
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse=False)
ohe.fit_transform(df[["nom_0"]])
le=LabelEncoder()
df["nom_0"]=le.fit_transform(df[["nom_0"]])
df

from sklearn.preprocessing import StandardScaler
sc=StandardScaler()
df1=pd.DataFrame(sc.fit_transform(df),columns=['id','bin_1','bin_2','nom_0','Ord_2'])
df1

from sklearn.preprocessing import MinMaxScaler
mms=MinMaxScaler()
df2=pd.DataFrame(mms.fit_transform(df),columns=['id','bin_1','bin_2','nom_0','Ord_2'])
df2

from sklearn.preprocessing import MaxAbsScaler mas=MaxAbsScaler()
df3=pd.DataFrame(mas.fit_transform(df),columns=['id','bin_1','bin_2','nom_0','Ord_2'])
df3

from sklearn.preprocessing import RobustScaler
rs=RobustScaler()
df4=pd.DataFrame(rs.fit_transform(df),columns=['id','bin_1','bin_2','nom_0','Ord_2'])
df4
```
# OUTPUT:
## Given DataFrame:
![166729007-0ceab8b8-4f62-488f-a84c-81f6c684798e](https://user-images.githubusercontent.com/94169318/167535752-06f9cdf1-7e81-4a56-90ff-1e4aba63797a.png)

## Feature encoding using Ordinal Encoder:
![166729063-c40908a2-a634-4906-b244-3355148a876c](https://user-images.githubusercontent.com/94169318/167535782-e587b16c-9fe3-429f-9388-a0c0df06de3c.png)

## Feature encoding using Binary Encoder:
![166729091-fc413c9d-1c5e-43f5-a543-bbafba721ca2](https://user-images.githubusercontent.com/94169318/167535808-0cb9bb16-c57f-4e41-898f-3ae93b54192d.png)
![166729162-334ced7d-d2f6-44bc-9446-406396b98ec7](https://user-images.githubusercontent.com/94169318/167535819-c8af8977-64b3-402c-8c92-538d30387180.png)

## Feature encoding using One Hot Encoder:
![166729207-8d03c979-0023-4e78-9595-8ce77206bcb4](https://user-images.githubusercontent.com/94169318/167535847-27bcc761-c846-4e9b-b8b5-ffe51552b3b7.png)

## Feature encoding using Label Encoder:
![166867603-52ef9b02-9f21-497a-b9ef-a137dfcdafe8](https://user-images.githubusercontent.com/94169318/167535894-76fc3945-30ee-4f75-8a7f-7e12e192b364.png)

## Feature scaling using Standard Scaler:
![166729355-c096d36e-4f6e-4582-9058-74b9f456c473](https://user-images.githubusercontent.com/94169318/167535950-80275b88-9936-485f-aaba-6d26b442ca2e.png)

## Feature scaling using MinMax Scaler:
![166729401-72c8c12b-f871-4a65-9ed7-d8f78b6e5383](https://user-images.githubusercontent.com/94169318/167535995-512feb0e-bf28-483d-a995-761f5b5a47f1.png)

## Feature scaling using MaxAbs Scaler:
![166729449-3b1d9948-a61f-4ab9-a3b2-3c4444838a2f](https://user-images.githubusercontent.com/94169318/167536024-910399b0-4bbf-447e-96ab-6fbe6214faa1.png)

## Feature scaling using Robust Scaler:
![166729528-26ddceb7-5d74-4be9-8626-365570616da8](https://user-images.githubusercontent.com/94169318/167536058-7c444df8-d262-435d-b946-0edd91313c90.png)

# 3.FEATURE GENERATION FOR titanic_dataset.csv
## CODE FOR FEATURE ENCODING AND FEATURE SCALING:
```
import pandas as pd
df=pd.read_csv("titanic_dataset.csv")
df
df.isnull().sum()
df["Age"]=df["Age"].fillna(df["Age"].median())
df["Embarked"]=df["Embarked"].fillna(df["Embarked"].mode()[0])
df
df.drop("Cabin",axis=1,inplace=True)
df.drop("Ticket",axis=1,inplace=True)
df.drop("Name",axis=1,inplace=True)
df.isnull().sum()
df
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
embark=["C","S","Q"]
emb=OrdinalEncoder(categories=[embark])
df["Embarked"]=emb.fit_transform(df[["Embarked"]])
df
from category_encoders import BinaryEncoder
be=BinaryEncoder()
df["Sex"]=be.fit_transform(df[["Sex"]])
df

from sklearn.preprocessing import StandardScaler
ss=StandardScaler()
df1=pd.DataFrame(ss.fit_transform(df),columns=['Passenger','Survived','Pclass','Sex','Age','SibSp','Parch','Fare','Embarked','PClass'])
df1

from sklearn.preprocessing import MinMaxScaler
mms=MinMaxScaler()
df2=pd.DataFrame(mms.fit_transform(df),columns=['Passenger','Survived','Pclass','Sex','Age','SibSp','Parch','Fare','Embarked','PClass'])
df2

from sklearn.preprocessing import MaxAbsScaler
mas=MaxAbsScaler()
df3=pd.DataFrame(mas.fit_transform(df),columns=['Passenger','Survived','Pclass','Sex','Age','SibSp','Parch','Fare','Embarked','PClass'])
df3

from sklearn.preprocessing import RobustScaler
rs = RobustScaler()
df4=pd.DataFrame(rs.fit_transform(df),columns=['Passenger','Survived','Pclass','Sex','Age','SibSp','Parch','Fare','Embarked','PClass'])
df4
```

# OUTPUT:
## Given DataFrame:
![166729907-864f67a2-292b-46b5-86b0-623fc95d4018](https://user-images.githubusercontent.com/94169318/167536194-5b47b956-e449-40ee-a02d-2565feeb4d51.png)

## Resolving null value data:
![166729987-bf3f0ef2-7b33-45c6-9a28-4d2f81fa93f5](https://user-images.githubusercontent.com/94169318/167536225-abe4776c-87fb-4642-aa0b-6e690a1f2047.png)
![166730122-66bbb495-5eb3-4acd-a88c-7440695fdb1e](https://user-images.githubusercontent.com/94169318/167536245-aae9d19e-11a2-4e70-9e6c-0383591064d0.png)

## Dropping unnecessary columns:
![166730193-45f7ac31-6721-4963-a927-b7316dd303be](https://user-images.githubusercontent.com/94169318/167536275-599be3bd-d863-4da0-aa93-15611815cb3e.png)

## Feature encoding using Ordinal Encoder:
![166730320-a6bd2ef5-c792-44f7-b228-0b2d2cf2378d](https://user-images.githubusercontent.com/94169318/167536305-097a0fa2-8b24-4dc1-abc6-54ce2a2d0b75.png)

## Feature encoding using Binary Encoder:
![166730455-633c31e1-eb74-41f1-97b2-2c84db36a55b](https://user-images.githubusercontent.com/94169318/167536425-9323e011-bf51-4328-a1e4-80998846ab59.png)

## Feature scaling using Standard Scaler:
![166730587-ac41dd9c-0ad5-46e0-96d3-655f7ff448b9](https://user-images.githubusercontent.com/94169318/167536485-746e1c58-fb1b-44be-8df8-831d73cae0ac.png)

## Feature scaling using MinMax Scaler:
![166730692-10c6f980-76b4-4195-ae2e-b74a9b7b4dae](https://user-images.githubusercontent.com/94169318/167536521-94b2f6e4-909b-49c0-8195-677003e2f5cd.png)

## Feature scaling using MaxAbs Scaler:
![166730836-8994554a-cd85-42a5-9af1-7525d545aba4](https://user-images.githubusercontent.com/94169318/167536551-0d06705a-5556-4b67-b83e-f3a72e60705d.png)

## Feature scaling using Robust Scaler:
![166730944-2cd8f869-adc5-45cd-9374-cf046cfecd9c](https://user-images.githubusercontent.com/94169318/167536578-b2c7063b-9c07-4084-8d71-8c3dc54d9e33.png)

# RESULT:
Feature Encoding process and Feature Scaling process is applied to the given data frame sucessfully.
