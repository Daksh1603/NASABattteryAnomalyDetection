<img src="MachineB.jpg" width="1600px" height="200px">

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



+ <p style="color:#00704A">DBSCAN</p> A total of **14,218** anomalies were detected using this method . The following method makes use of a SOTA clustering method in order to classify anomalies . Eventough more accurate and resultfull than IQR Elimination , it still underperforms Isolation Forests for anomaly detection .

	Results of DBSCAN visualised :

+ <p style="color:#00704A">Isolation Forests</p>  An average total of **5,573** anomalies were detected using this method . These methods classify anomalies based on their scores through creating an ensemble of classification trees . These scores vary for different values of contamination , and the contamination values directly corresponds to confidence in anomaly classificaiton . Anomaly Score directly scales with contamination value .

Results of Isolation Forests visualised :
