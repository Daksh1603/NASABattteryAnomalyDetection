<img src="https://user-images.githubusercontent.com/90456255/212345055-b4f0361d-a563-4e36-a7a9-b4cff00a024b.jpg" width="1600px" height="200px">

<p style="text-align: center;color:#FD6A02;font-size:25px;"><strong>Introduction</strong></p>

The following datasets consists of records of 4 Hydrogen Fuel Cells built for FCEV in space exploration .These fuel cells provide with electric power with hydrogen on-board .

The Data Scientist Team at NASA wanted to **understand the aging process , charge and discharge cycles of the the cell** and in order to do so , they install certain sensors that measure parameters of these cells each time they are in use . Here , we try to understand these parameters and **instance out anomalities to understand abnormalities** and in order to aid with streamlined and error free research, maintenance and development of these cells .

<p style="text-align: center;color:#FD6A02;font-size:25px;"><strong>Data</strong></p>

The dataset consists of : 

- <em>nasaBattery.csv</em> - this file contains continuous records of multiple batteries , their sensor values, until they were deemed in a functionless state. ( 185,720 instances distributed over 4 batteries ) 

 <p style="text-align: center;color:#FD6A02;font-size:25px;"><strong>Methodology</strong></p>
 
 1. <p style="color:#FD6A02">The first and foremost step is to understand the problem statement entirely and make important deductions based on the statement .</p>


	+ What are we trying to find out ? What other attributes mean and represent , their types .
  	+ What are the important factors affecting the following ?
 	+ Cleaning the data to make sure there is no irregularity . 
 
 
2. <p style="color:#FD6A02">Importing the required libraries .</p>

3. <p style="color:#FD6A02">Loading the data .</p>

+ The data is loaded into a dataframe .
 	
+ For further analysis of these data and how they correlate with each other , we can merge them and then analyse them further however , I usually extend this part to EDA and not in Loading the Data because the data we have just received might not be perfect . It is not right to make dedcutions without clearing your assumptions on the data and without cleaning it .



4. <p style="color:#FD6A02">Data Engineering</p>

	+ Time series dataset contains in it a lot of information . A lot of independent factors (day_of_week, day, month, hour...) and dependent factors (voltage_chg, current_mean, temperature_median...) can be deduced . Hence carefull data engineering is an integral part of this porject .
	+ Further , cleaning and transforming the data further prerares it for EDA . 
 
   >  Do keep in mind that data transormation here doesn't refer to minmax scaling or normalization . Simply conversion of irregular attributes to derive more regular attributes ( for example : dict value from offer Data ) .


5. <p style="color:#FD6A02">Exploratory Data Anlaysis</p>

	+ The following step involves getting to know your data to your full extent . Here , I try and visualise the data in order to bring important deductions that may help me in developing my model more effeciently .
	+ The following part is taken care of and explained in the `ipynb file` .

6. <p style="color:#FD6A02">Outlier Visualistion through Boxplots</p>

	+ Making use of standard boxplots for various sensors values in order to detect standard outliers through standard defination .


7. <p style="color:#FD6A02">Anomaly Scanning</p>

   + Implementing 3 different methods to scan .
   + Visualising the outcomes of these plots .

<p style="text-align: center;color:#00704A;font-size:25px;"><strong>Results</strong></p>

The 3 most important methods deployed for anomaly detection and their results were  :

+ <p style="color:#00704A">Inter-Quartile Range Elimination</p>  A total of **37,766** anomalies were detected using this method . Most of the data removed might not essential be outliers since multiple factors (engineered at the start of this project) might affect its classification . However, IQR doesn't consider these factors and classifies on the basis of hard and fast pre defined formula / rule leading to data loss .

	Results of IQR Elimination visualised :
![IQR1](https://user-images.githubusercontent.com/90456255/212345106-a5046ad9-9b07-4a08-9070-be356a018fef.png)
![IQR2](https://user-images.githubusercontent.com/90456255/212345114-ac5c5697-06a4-4f0a-8fdf-bf6ff3089c80.png)
![IQR3](https://user-images.githubusercontent.com/90456255/212345124-0b5050d7-5683-4202-b5fb-a1aa95669fbb.png)

+ <p style="color:#00704A">DBSCAN</p> A total of **14,218** anomalies were detected using this method . The following method makes use of a SOTA clustering method in order to classify anomalies . Eventough more accurate and resultfull than IQR Elimination , it still underperforms Isolation Forests for anomaly detection .

	Results of DBSCAN visualised :
![DB1](https://user-images.githubusercontent.com/90456255/212345143-01004890-a9b7-428d-9e56-8352be6e89a7.png)
![DB2](https://user-images.githubusercontent.com/90456255/212345150-68f801d3-cdf6-47b1-8d64-5ee2d814834c.png)
![DB3](https://user-images.githubusercontent.com/90456255/212345163-a41f44a1-1c30-46d2-b722-3bd1f61da94a.png)

+ <p style="color:#00704A">Isolation Forests</p>  An average total of **5,573** anomalies were detected using this method . These methods classify anomalies based on their scores through creating an ensemble of classification trees . These scores vary for different values of contamination , and the contamination values directly corresponds to confidence in anomaly classificaiton . No. of anomalies directly scales with contamination value .

	Results of Isolation Forests visualised :
![Iso1](https://user-images.githubusercontent.com/90456255/212345213-415e3e89-47b5-4ca0-8ebc-5a98e2ba3831.png)
![Iso2](https://user-images.githubusercontent.com/90456255/212345237-129cafaf-1f32-48d0-96f8-8e484c4776e3.png)

> Red extreme of the cmap corresponds to critical anomalies .
> Green extreme of the cmap corresponds to normal data .

![Iso3](https://user-images.githubusercontent.com/90456255/212345248-b0f6ab1d-3c2a-435c-b9ea-7040ea5c2dab.png)
![Iso4](https://user-images.githubusercontent.com/90456255/212345263-bdecc247-caf4-4018-ad11-04f43cb1dc38.png)
