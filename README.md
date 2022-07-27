# Repository_francis

## Project Description
This project is detecting anomalies in the extrusion process, via AI apporach. Since the factors that affect quality of the proecut are product parameters, and defects, detecting defects in the process is vital for high quality. However, the defects are detected unefficiently; only through operators, and not even in real time. Therefore, AI technologies could derive efficient ways to distinguish those deficiencies.

![Schematic_of_metal_extrusion_process](https://user-images.githubusercontent.com/100813293/181161238-4d29b214-ecb5-43f4-9420-a06f2d0cde96.jpeg)

## Data Collection Description
The dataset is collected from the Kaggle website, which is available at <https://www.kaggle.com/datasets/podsyp/find-a-defect-in-the-production-extrusion-line>. The dataset consists of 226536 rows and 481 columns. Since the dataset does not contain a target column, the target column is determined referring to this website, <https://www.kaggle.com/code/monikaeliaszkowalska/six-sigma-project-on-malfunction>. In short, film thickness is predominant factor in the manufacturing process, therefore the author cliams that if the thickness of the film is 0, then it will be defects. Therefore, in this project, the target column was chosen through the same process . 

```
! mkdir ~/.kaggle
! cp kaggle.json ~/.kaggle/
! chmod 600 ~/.kaggle/kaggle.json
! kaggle datasets download podsyp/find-a-defect-in-the-production-extrusion-line
```
![count_image](https://user-images.githubusercontent.com/100813293/181160443-1bd74c1e-f73c-4e0f-803e-e8feb795be7d.png)

<img width="1253" alt="KakaoTalk_Photo_2022-07-27-13-16-50" src="https://user-images.githubusercontent.com/100813293/181160437-b394ef7f-c0a6-432b-829d-aec4e303a984.png">

## Experiment Design
Since the format of the given dataset is csv, machine learning algorithms were utilized. The target column consists of 196006 normal ones, and 29428 anomaly ones, respectively. The experiment consists of two steps:
- In the first step, normal machine learning classifiers such as LGBM, Random Forest will be utilized. 
- Then, since the objective of this project is to identify the anomaly ones, those algorithms which are specialized at anomaly detections were utilized, such as Isolation Forest. 

### Data Preprocessing
- Check Null values and drop them
- Feature engineering: Extract "month", "year", "date" from "Datum" column
- EDA: Figure out if there exists any certain pattern in the dataset
- Correlaion Function: Discover certain columns which have high correlations with the target
- PCA: Reduce the dimension of the given dataset, and discard those high correlated columns 

![EDA](https://user-images.githubusercontent.com/100813293/181160442-03470094-1ffb-4e0e-97f3-6974ac3a5ac0.png)
![eda_month](https://user-images.githubusercontent.com/100813293/181160990-fb7a0925-3563-4728-b10f-4cbc041117fd.png)


## Result
Comparing the results from the first and second experiments, it could be concluded that the machine learning classifiers used in the first expeirments surpassed the anomaly detection algorithms, which were utilized in the second expeirment. The below paragh describes the representative results from each experiment. 

![graph](https://user-images.githubusercontent.com/100813293/181160440-7a8f503b-e924-4ba3-9859-a6166c0b2a61.png)

- Random Forest: 
  - Accuracy Score: 1.00
  - Precision Score: 0.99
  - Recall Score: 0.99
  - F1 Score: 0.99
  
- Isolation Forest:
  - Accuracy Score: 0.85
  - Precision Score: 0.67
  - Recall Score: 0.7
  - F1 Score: 0.68 

## Reference
https://commons.wikimedia.org/wiki/File:Schematic_of_metal_extrusion_process.jpg
https://www.kaggle.com/code/monikaeliaszkowalska/six-sigma-project-on-malfunction
https://www.kaggle.com/datasets/podsyp/find-a-defect-in-the-production-extrusion-line
