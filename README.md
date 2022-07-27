# Repository_francis

## Project Description
This project is detecting anomalies in the extrusion process, via AI apporach. Since the factors that affect quality of the proecut are product parameters, and defects, detecting defects in the process is vital for high quality. However, the defects are detected unefficiently; only through operators, and not even in real time. Therefore, AI technologies could derive efficient ways to distinguish those deficiencies.

## Data Description
The dataset is collected from the Kaggle website, which is available at <https://www.kaggle.com/datasets/podsyp/find-a-defect-in-the-production-extrusion-line>. The dataset consists of 226536 rows and 481 columns. Since the dataset does not contain a target column, the target column is determined referring to this website, <https://www.kaggle.com/code/monikaeliaszkowalska/six-sigma-project-on-malfunction>. In short, film thickness is predominant factor in the manufacturing process, therefore the author cliams that if the thickness of the film is 0, then it will be defects. Therefore, in this project, the target column was chosen through the same process . 
```
plt.figure(figsize=(8,6))
plt.hist(data[data['ST110_VAREx_0_SDickeIst'] < 100]['ST110_VAREx_0_SDickeIst'], bins=100, alpha=0.5, label="extruder 0")
plt.hist(data[data['ST110_VAREx_1_SDickeIst'] < 100]['ST110_VAREx_1_SDickeIst'], bins=100, alpha=0.5, label="extruder A")
plt.hist(data[data['ST110_VAREx_2_SDickeIst'] < 100]['ST110_VAREx_2_SDickeIst'], bins=100, alpha=0.5, label="extruder B")
plt.hist(data[data['ST110_VAREx_3_SDickeIst'] < 100]['ST110_VAREx_3_SDickeIst'], bins=100, alpha=0.5, label="extruder C")
plt.xlabel("Data", size=14)
plt.ylabel("Count", size=14)
plt.title("Different extruders and actual layer thickness")
plt.legend(loc='upper right')
```
```
data['EXT0'] = data['ST110_VAREx_0_SDickeIst'].apply(lambda x: 1 if x == 0 else 0)
data['EXTA'] = data['ST110_VAREx_1_SDickeIst'].apply(lambda x: 1 if x == 0 else 0)
data['EXTB'] = data['ST110_VAREx_2_SDickeIst'].apply(lambda x: 1 if x == 0 else 0)
data['EXTC'] = data['ST110_VAREx_3_SDickeIst'].apply(lambda x: 1 if x == 0 else 0)
data['EXTsum'] = data['EXTC']+data['EXTA']+data['EXTB']+data['EXT0']
data['EXTtotal'] = data['EXTsum'].apply(lambda x: 0 if x == 0 else 1)`
```
## Experiment Design
Since the format of the given dataset is csv, machine learning algorithms were utilized. The target column consists of 196006 normal ones, and 29428 anomaly ones, respectively. The experiment consists of two steps: in the first step, normal machine learning classifiers such as LGBM, Random Forest will be utilized. Then, since the objective of this project is to identify the anomaly ones, those algorithms which are specialized at anomaly detections were utilized, such as Isolation Forest. Before utilizing those aglorithms, several data preprocessing, and EDA methods were utilized and those procedures could be found in the source code. For instance, the PCA algorihtm was used applied to the dataset, since the dataset contains multiple high correlated features. 
```
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

scaler=StandardScaler().fit(pred)
pred=scaler.transform(pred)

pca=PCA(n_components=5)
principalComponents=pca.fit_transform(pred)
pca_result=pd.DataFrame(data= principalComponents, columns = ['principal component 1', 'principal component 2', 'principal component 3', 'principal component 4', 'principal component 5'])
```

