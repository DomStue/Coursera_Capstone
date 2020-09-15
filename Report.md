##Introduction

The aim of the project is to predict the severity of car accidents by using data of former car accidents in the area of seattle. The labeled data has been obtained from 2004 to present and is updated one a weekly basis. A model calculated from this data to predict the severity of a car accident might be useful for emergency services such as paramedics or firefighters. Moreover, it might be useful to provide information for insurances and therefore might be helpful to prevent insurance fraud.

##The data

The data comprises of 194673 total entries and the number of categories or parameters is 37. The severity of the car accidents is measured as a categorical number, which means a supervised classification model is used for this dataset. Although the scale goes from 0 to 3, only entries with 1(prop damage) and 2 (injury) are included. The categories include several information about the accident, like the location, persons and cars involved, injuries of persons, the type of collisions, the road, wheather or light conditions and time and dates.

Data will be explored for missing entries and if they include valuable, causal information which may effect the severity of the car accidents. Afterwards, a classification model such as KNN, SVM, Logistic Regression or Decision will be applied.

##The Methodology

Since 37 is a very huge parameter set and some of them might redundant (for example coordinates and adress), only few parameters are selected from the dataset for the features in our model. Severity code will (SEVERITYCODE) will be our target array. The selected features are ['ADDRTYPE','SEVERITYDESC','COLLISIONTYPE','PERSONCOUNT','PEDCOUNT','PEDCYLCOUNT','VEHCOUNT','INCDTTM','JUNCTIONTYPE','INATTENTIONIND','UNDERINFL','WEATHER', 'LIGHTCOND', 'ROADCOND','PEDROWNOTGRNT','SPEEDING','SEGLANEKEY','CROSSWALKKEY','HITPARKEDCAR'] and you can look up their meanings at https://s3.us.cloud-object-storage.appdomain.cloud/cf-courses-data/CognitiveClass/DP0701EN/version-2/Metadata.pdf.

The date time feature is transformed to hour of the data and the weekday information. Afterwards the features are investigated for empty entries:

ADDRTYPE            1926
SEVERITYDESC           0
COLLISIONTYPE       4904
PERSONCOUNT            0
PEDCOUNT               0
PEDCYLCOUNT            0
VEHCOUNT               0
JUNCTIONTYPE        6329
INATTENTIONIND    164868
UNDERINFL           4884
WEATHER             5081
LIGHTCOND           5170
ROADCOND            5012
PEDROWNOTGRNT     190006
SPEEDING          185340
SEGLANEKEY             0
CROSSWALKKEY           0
HITPARKEDCAR           0
WEEKDAY                0
HOURDAY                0

As you can see, there are several features with a significant amount of missing values. Those empty entries are filled with illed with 'No', 'Unknown' and 'Other' values (depending on the feature). Unknown and Other are values are combined in each feature. Features are then one-hot-encoded, which results in a features array with 194673 rows and 55 features in total. To reduce the number of features (preventing overfitting and reducing computation time), feature selectio is applied using the Chi2-Score of each feature.

The best 20 features are:

8                              CROSSWALKKEY  3.186417e+09
7                                SEGLANEKEY  8.638549e+07
15                         Injury Collision  1.364850e+05
20                               Parked Car  1.356930e+04
1                                  PEDCOUNT  1.248884e+04
21                               Pedestrian  1.132928e+04
2                               PEDCYLCOUNT  8.818806e+03
17                                   Cycles  8.608345e+03
5                             PEDROWNOTGRNT  8.085270e+03
26   At Intersection (intersection related)  5.360734e+03
14                             Intersection  5.137017e+03
29  Mid-Block (not related to intersection)  2.939348e+03
22                               Rear Ended  2.811283e+03
0                               PERSONCOUNT  2.473877e+03
24                                Sideswipe  2.395238e+03
13                                    Block  2.312244e+03
9                              HITPARKEDCAR  1.931147e+03
16                                   Angles  1.462505e+03
11                                  HOURDAY  9.587739e+02
46                                 Daylight  6.028858e+02

This gives insight which parameters play an important role in determing the Severity of an accident. For example it is very important, if the accident happend at a crosswalk, if parking cars were involved, if pedestrians or cyclist have been involved, the number of involved persons and injuries. These 20 features are then scaled and transformed to to train KNN, A Decision Tree, SVM and a logistic regression. The size of our test data is only 1% of the entire data set. The results are shown in the following table:

Algorithm	          Accuracy	Jaccard	  F1-score
KNN	                0.998973	0.998973	0.998973
Decision Tree	      1.000000	1.000000	1.000000
SVM	                0.999486	0.999486	0.999487
LogisticRegression	1.000000	1.000000	1.000000

Which shows the very good accuracy for each of the models.

###Results, Discussion and Conclusion

The trained model showed an excellent performance and can therefore be used for the desired applications like paramedical applications or insurance related applications. However, one might get a similar result using less parameter and therefore less computation time. Therefore, one should try to further reduce the parameterset.
