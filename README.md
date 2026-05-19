## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
## Encoding:
```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv('data.csv')
print(df)
```
<img width="617" height="252" alt="image" src="https://github.com/user-attachments/assets/580ef952-6b2a-43b3-93bd-2632bd99da85" />

## Ordinal Encoding:
```
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
climate = ['Cold','Warm','Hot','Very Hot']
ele = OrdinalEncoder(categories=[climate])
ele.fit_transform(df[["Ord_1"]])
```
<img width="192" height="225" alt="image" src="https://github.com/user-attachments/assets/5cac8d13-bfcf-4e57-a071-ba3ace16bd08" />

```
df['bo2'] = ele.fit_transform(df[["Ord_1"]])
df
```
<img width="565" height="375" alt="image" src="https://github.com/user-attachments/assets/ffe0b796-8ebb-4c32-92a9-1d7d67d58c30" />

## Label Encoding:
```
le = LabelEncoder()
df2 = df.copy()
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```
<img width="503" height="388" alt="image" src="https://github.com/user-attachments/assets/8da3c91a-c903-47e5-8ba7-3ef53c23ec65" />

```
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```
<img width="467" height="386" alt="image" src="https://github.com/user-attachments/assets/156a04b4-7d95-4f5e-af32-a2c63762d5b4" />

## OneHot Encoding:
```
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder()
df3 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2 = pd.concat([enc,df3],axis = 1)
df2
```
<img width="560" height="377" alt="image" src="https://github.com/user-attachments/assets/a8dcd759-53e0-4769-ba09-258ef20f50a1" />

```
pd.get_dummies(df,columns=['City'])
```
<img width="866" height="377" alt="image" src="https://github.com/user-attachments/assets/18473ff8-415e-4567-a33d-6a6d920356f1" />

## Binary Encoding:
```
from category_encoders import BinaryEncoder
df = pd.read_csv('data.csv')
df
```

```
be = BinaryEncoder()
nd = be.fit_transform(df['Ord_2'])
df
```

## Target Encoding:
```
from category_encoders import TargetEncoder
te = TargetEncoder()
CC = df.copy()
new = te.fit_transform(CC["City"],y=CC["Target"])
CC = pd.concat([CC,new],axis = 1)
CC
```

```
if 'City' in CC.columns:
    CC = CC.drop('City', axis=1)
new = te.fit_transform(X = df["City"],y=df["Target"])
CC = pd.concat([CC.reset_index(drop=True),new.reset_index(drop=True)],axis = 1)
CC
```

## Transformation
```
df = pd.read_csv('Data_to_Transform.csv')
df
```
<img width="750" height="473" alt="image" src="https://github.com/user-attachments/assets/85630e91-aedd-451f-be10-b1a95e69de88" />

```
df.skew()
```
<img width="412" height="125" alt="image" src="https://github.com/user-attachments/assets/43fbf3c6-0b8a-45d7-831f-e86a8fef5a64" />

## Function Transformation:
```
np.log(df["Highly Positive Skew"])
```
<img width="587" height="275" alt="image" src="https://github.com/user-attachments/assets/3fd809db-416b-4e0e-be05-4f6f481e1880" />

```
np.reciprocal(df["Moderate Positive Skew"])
```
<img width="586" height="267" alt="image" src="https://github.com/user-attachments/assets/f8381ef7-4ec2-474b-91b7-32688da6bb53" />

```
np.sqrt(df["Highly Positive Skew"])
```
<img width="567" height="270" alt="image" src="https://github.com/user-attachments/assets/4afc3c27-e505-422d-a9d9-194256476016" />

```
np.square(df["Highly Positive Skew"])
```
<img width="575" height="267" alt="image" src="https://github.com/user-attachments/assets/1275645d-6ae7-478e-8b39-ea7e198d64f3" />

## Power Transformation
```
df["Highly Positive Skew_boxcox"], parameters = stats.boxcox(df["Highly Positive Skew"])
df
```
<img width="750" height="458" alt="image" src="https://github.com/user-attachments/assets/a17615e4-b2a5-4b60-bd19-cb456373fbff" />

```
df["Moderate Negative Skew_yeojohnson"], parameters = stats.yeojohnson(df["Moderate Negative Skew"])
df
```
<img width="750" height="490" alt="image" src="https://github.com/user-attachments/assets/ee9ed23c-1050-40a6-bc29-b31bf2b8b90a" />

```
from sklearn.preprocessing import QuantileTransformer
qt = QuantileTransformer(output_distribution = 'normal')
df["Moderate Negative Skew_1"] = qt.fit_transform(df[["Moderate Negative Skew"]])
df

```
<img width="741" height="488" alt="image" src="https://github.com/user-attachments/assets/64b82e6a-409f-4a94-a400-92d9e95ed613" />

```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df["Moderate Negative Skew"],line = '45')
plt.show()
```
<img width="748" height="556" alt="image" src="https://github.com/user-attachments/assets/c4b6216e-878c-4198-ba8d-06fc1e5c87aa" />

```
sm.qqplot(df["Moderate Negative Skew_1"],line = '45')
plt.show()
```


```
df["Highly Negative Skew_1"] = qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line = '45')
plt.show()
```


```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line = '45')
plt.show()
```


```
sm.qqplot(df["Highly Negative Skew_1"],line = '45')
plt.show()
```

```
sm.qqplot(np.abs(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```

```
sm.qqplot(np.log(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```

```
sm.qqplot(np.sqrt(df["Moderate Negative Skew_1"]),line='45')
plt.show()
```

```
pd.concat([CC,new],axis = 1)
```

# RESULT:
Thus, we have successfully performed Feature Encoding and Transformation process and saved the data to a file.


       
