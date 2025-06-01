## EXNO-3-DS
### Name : ABDUR RAHMAN BASIL A H
### Reg No : 212223040002
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
### Feature Encoding:
### OrdinalEncoder:
```py
from sklearn.preprocessing import OrdinalEncoder
ordinal_order = [['unfurnished', 'semi-furnished', 'furnished']]
ordinal_encoder = OrdinalEncoder(categories=ordinal_order)
df['furnishingstatus_ordinal'] = ordinal_encoder.fit_transform(df[['furnishingstatus']])
df[['furnishingstatus', 'furnishingstatus_ordinal']].head()
```
![image](https://github.com/user-attachments/assets/1f564263-30ce-4959-8d45-26906b89eb17)
### LabelEncoder:
```py
from sklearn.preprocessing import LabelEncoder

label_encoder = LabelEncoder()
df['mainroad_label'] = label_encoder.fit_transform(df['mainroad'])
df[['mainroad', 'mainroad_label']].head()
```
![image](https://github.com/user-attachments/assets/01dc304f-8e97-41d3-b842-490f696cc1e1)
### BinaryEncoder:
```py
import category_encoders as ce
binary_encoder = ce.BinaryEncoder(cols=['furnishingstatus'])
df_binary = binary_encoder.fit_transform(df['furnishingstatus'])

df = pd.concat([df, df_binary], axis=1)
df_binary.head()
```
![image](https://github.com/user-attachments/assets/b28075a6-766e-407d-b949-97dee39e92d3)
### One hot Encoding:
```py
df_onehot = pd.get_dummies(df, columns=['furnishingstatus'], drop_first=True)
df_onehot.head()
```
![image](https://github.com/user-attachments/assets/79072708-3362-4d8b-9d86-e8f3edf167b5)

### Data Transformation:
```py
from sklearn.preprocessing import PowerTransformer
from scipy.stats import boxcox
# Area transformations
df['log_area'] = np.log1p(df['area'])                     # log(1 + x)
df['reciprocal_area'] = 1 / (df['area'] + 1)              # avoid division by zero
df['sqrt_area'] = np.sqrt(df['area'])
df['square_area'] = df['area'] ** 2
# Box-Cox requires positive values
df['boxcox_area'], _ = boxcox(df['area'])

# Yeo-Johnson (safe for 0 or negative values too)
pt_yeo = PowerTransformer(method='yeo-johnson')
df['yeojohnson_area'] = pt_yeo.fit_transform(df[['area']])

df['sqrt_parking'] = np.sqrt(df['parking'])

pt_parking = PowerTransformer(method='yeo-johnson')
df['yeojohnson_parking'] = pt_parking.fit_transform(df[['parking']])

transformed_cols = ['log_area', 'reciprocal_area', 'sqrt_area', 'square_area', 'boxcox_area', 
                    'yeojohnson_area', 'sqrt_parking', 'yeojohnson_parking']
for col in transformed_cols:
    plt.figure(figsize=(6, 4))
    sm.qqplot(df[col], fit=True, line='45')
    plt.title(f"Q-Q Plot - {col}")
    plt.tight_layout()
    plt.show()
```
### Output:
![image](https://github.com/user-attachments/assets/69b3bf16-2161-4aae-9944-936c1d335d43)
![image](https://github.com/user-attachments/assets/0a4d3372-db7e-492b-8262-9c8b6a9fcc85)
![image](https://github.com/user-attachments/assets/662332a3-3d99-4087-a1c2-5e9ab4780400)
![image](https://github.com/user-attachments/assets/ae07a454-d470-4a8e-8265-4e9399d512af)

# RESULT:
Thus Feature Encoding and Transformation process was performed successfully.
       
