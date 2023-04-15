BI-Project
Data Visualization With Power BI
Objectives:1
•	Using R to Import Raw Data
•	Clean Raw Data 
•	Outlier removal
•	Exploratory Data Analysis
•	Export Clean Data

Objectives:2
IMPORT clean_df.csv file into power B1
Create Power BI Dashboard that displays the following information listed below:
•	The average Rotten Tomatoes ratings of each genre
•	The number of movies produced per year 
•	The audience scores for each film  
•	The profitability per studio 
•	The worldwide gross per genre 

Task in R
1.	Data was downloaded from source: as seen in the screenshot below.
	![image](https://user-images.githubusercontent.com/103393876/232202902-a659e783-853d-495f-838d-0bd1de2f4c01.png)
2.	Downloaded excel file: as seen in the screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232202922-42f0e798-32b5-49c0-ab70-16ffb5d263ae.png)

3. The data was loaded/imported into are using the codes line df<- read.csv(“https://public.tableau.com/app/sample-data/HollywoodsMostProfitableStories.csv") as seen in the screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232202958-773d5ec9-b821-42d0-908c-00a843d0b55c.png)


4.	The data was looked at by using the following codes: View(df) as seen in the screenshot below.
	![image](https://user-images.githubusercontent.com/103393876/232202968-5c54ec53-1197-42c6-b46c-7e1f7b627153.png)

5.	The Tidyverse library was installed using the following codes: install.packages("tidyverse")  was install in R. As in the screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232202988-9d87a481-261a-41d4-a728-5aa040010433.png)

6.	The data type was checked using the following codes: str(df). The screen shot show the data type. 
 ![image](https://user-images.githubusercontent.com/103393876/232203000-3a74b41d-9ec5-4c6b-b7eb-af416585968d.png)


Step 2: Clean Data 

1.	Th following codes was used to Check for missing values: colSums(is.na(df) as seen in screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232203025-09bb5b9d-4e52-40c7-9a63-d7b8050c15d2.png)

2.	Th following codes was used to Drop missing values : df <- na.omit(df) as seen in screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232203012-77e5b33d-edf3-45c7-8be4-ebb6751f7883.png)

3. The following codes was used to check to make sure that the rows have been removed colSums(is.na(df)) as seen in screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232203031-fe842668-4728-42b4-ada6-b532a2e84c19.png)

4.	The following codes was used to Check for duplicates 
dim(df[duplicated(df$Film),])[1] as seen in screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232203051-e8b1fca0-a1f8-4b54-86aa-f2f1b71f0a20.png)

5.	 The following codes was used to round off values to 2 places   

df$Profitability <- round(df$Profitability ,digit=2) as seen in screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232203090-d3d7f880-4dea-4dc0-8d8e-b08f43381113.png)

df$Worldwide.Gross <- round(df$Worldwide.Gross ,digit=2) 
![image](https://user-images.githubusercontent.com/103393876/232203080-a036252f-d9c3-4e54-bb24-07bcf11b0d56.png)

6.	 The following codes was used 
View(df)  
dim(df) as seen in screenshot below.
![image](https://user-images.githubusercontent.com/103393876/232203117-fbc02384-6108-48da-bc62-b6b0e4cb4dd5.png)

Step 2.1: Outlier removal 
1.	 The following codes was used Check for outliers using a boxplot 
library(ggplot2) 
![image](https://user-images.githubusercontent.com/103393876/232203132-e8ff7962-b5d7-49dc-b04b-6bc79b7f55ab.png)

2.	The following codes was used to Create a boxplot that highlights the outliers   
ggplot(df, aes(x=Profitability, y=Worldwide.Gross)) + geom_boxplot(outlier.colour = "red", outlier.shape = 1)+ scale_x_continuous(labels = scales::comma)+coord_cartesian(ylim = c(0, 1000)) 
![image](https://user-images.githubusercontent.com/103393876/232203174-fa6f0f6c-84ac-45ce-85a0-148d836d41aa.png)

3.	 The following codes was used  to Remove outliers in 'Profitability' 
Q1 <- quantile(df$Profitability, .25) 

![image](https://user-images.githubusercontent.com/103393876/232203187-59e011f3-c5f0-40c2-a3ff-86930196e7e9.png)
Q3 <- quantile(df$Profitability, .75)

IQR <- IQR(df$Profitability) 
![image](https://user-images.githubusercontent.com/103393876/232203245-9cb5031b-15ff-4c15-96b1-beb11297d46b.png)

4. The following codes was used to: no_outliers <- subset(df, df$Profitability> (Q1 - 1.5*IQR) & df$Profitability< (Q3 + 1.5*IQR)) 
![image](https://user-images.githubusercontent.com/103393876/232203234-46897785-faf2-453f-aca6-962bd248dc11.png)

5.	The following codes was used dim(no_outliers)  
![image](https://user-images.githubusercontent.com/103393876/232203266-52d9c0db-662e-42be-bc06-1731dbaca0b2.png)

6.	The following codes was used to Remove outliers in 'Worldwide.Gross' 
Q1 <- quantile(no_outliers$Worldwide.Gross, .25) 

![image](https://user-images.githubusercontent.com/103393876/232203247-9f6e98e9-1390-4909-a97d-f1ea321ba26e.png)
Q3 <- quantile(no_outliers$Worldwide.Gross, .75) 
![image](https://user-images.githubusercontent.com/103393876/232203305-e33ca782-1535-4014-b220-7cbbcf5817f7.png)

IQR <- IQR(no_outliers$Worldwide.Gross) 
![image](https://user-images.githubusercontent.com/103393876/232203306-7ca90de0-61d9-4591-819b-8e9c038dd03b.png)
![image](https://user-images.githubusercontent.com/103393876/232203327-ac4b5e18-6bdb-4e9c-a4f7-97ab44183453.png)

The following codes was used: df1 <- subset(no_outliers, no_outliers$Worldwide.Gross> (Q1 - 1.5*IQR) & no_outliers$Worldwide.Gross< (Q3 + 1.5*IQR)) 

![image](https://user-images.githubusercontent.com/103393876/232203340-6ab687d2-590f-4252-bd37-8f2890b9d73f.png)
![image](https://user-images.githubusercontent.com/103393876/232203352-caedc8ab-c830-4f39-91af-035f4e4a6852.png)
The following codes was used  dim(df1)  
![image](https://user-images.githubusercontent.com/103393876/232203359-6d178973-3681-47f3-827e-dffbf483381a.png)

Step 3: Exploratory Data Analysis
1. The following codes was used to Summary Statistics/Univariate Analysis: 
summary(df1) 
![image](https://user-images.githubusercontent.com/103393876/232203379-de7d94b7-1a5f-48d6-954f-46252f08d55a.png)

2. The following codes was used to scatterplot:
ggplot(df1, aes(x=Lead.Studio, y=Rotten.Tomatoes..)) + geom_point()+ scale_y_continuous(labels = scales::comma)+coord_cartesian(ylim = c(0, 110))+theme(axis.text.x = element_text(angle = 90))
![image](https://user-images.githubusercontent.com/103393876/232203437-a1c81ea5-72e3-4f12-8adb-104a5504e5e1.png)

 The following codes was used bar chart:
ggplot(df1, aes(x=Year)) + geom_point() 
 ![image](https://user-images.githubusercontent.com/103393876/232203385-75e63416-f15a-4bcd-a738-93e1030c639a.png)
![image](https://user-images.githubusercontent.com/103393876/232203399-dfdfc12d-90fd-4512-91ce-00d3dc92da5f.png)

Step 4: Export data
1.	The following codes was used Export clean data:
write.csv(df1, “clean_df.csv")
![image](https://user-images.githubusercontent.com/103393876/232203481-aac6dcd0-a56f-4cfc-9a4f-5fa41ff1c897.png)
![image](https://user-images.githubusercontent.com/103393876/232203670-1482103f-e743-481c-9810-5c58b07b1ac3.png)

Power B1
1.	IMPORT clean_df.csv file into power B1
 ![image](https://user-images.githubusercontent.com/103393876/232203604-f29b3eda-e169-41e0-89f2-3bbe76cd69be.png)

2.	Transform data selected to view data.
 ![image](https://user-images.githubusercontent.com/103393876/232203548-de20c901-721d-4a99-be42-fd66a57786b5.png)

3.	Power BI Dashboard that displays the following information listed below:
•	The average Rotten Tomatoes ratings of each genre
•	The number of movies produced per year 
•	The audience scores for each film  
•	The profitability per studio 
•	The worldwide gross per genre 
![image](https://user-images.githubusercontent.com/103393876/232202863-1eea6172-5892-4e6e-89c7-0bb8879712c6.png)
https://app.powerbi.com/groups/me/reports/b6d0c62e-066c-45f6-9cf2-de5113c094c0/ReportSection18551c692d3cf57db2ad



