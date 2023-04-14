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
2.	Downloaded excel file: as seen in the screenshot below.
3.	The data was loaded/imported into are using the codes line df<- read.csv(“https://public.tableau.com/app/sample-data/HollywoodsMostProfitableStories.csv") as seen in the screenshot below.
4.	The data was looked at by using the following codes: View(df) as seen in the screenshot below.
5.	The Tidyverse library was installed using the following codes: install.packages("tidyverse")  was install in R. As in the screenshot below.
6.	The data type was checked using the following codes: str(df). The screen shot show the data type. 
 

Step 2: Clean Data 

1.	Th following codes was used to Check for missing values: colSums(is.na(df) as seen in screenshot below.
2.	Th following codes was used to Drop missing values : df <- na.omit(df) as seen in screenshot below.
3. The following codes was used to check to make sure that the rows have been removed colSums(is.na(df)) as seen in screenshot below.
4.	The following codes was used to Check for duplicates 
dim(df[duplicated(df$Film),])[1] as seen in screenshot below.
5.	 The following codes was used to round off values to 2 places   
df$Profitability <- round(df$Profitability ,digit=2) as seen in screenshot below.
df$Worldwide.Gross <- round(df$Worldwide.Gross ,digit=2) 
6.	 The following codes was used 
View(df)  
dim(df) as seen in screenshot below.

Step 2.1: Outlier removal 
1.	 The following codes was used Check for outliers using a boxplot 
library(ggplot2) 
2.	The following codes was used to Create a boxplot that highlights the outliers   
ggplot(df, aes(x=Profitability, y=Worldwide.Gross)) + geom_boxplot(outlier.colour = "red", outlier.shape = 1)+ scale_x_continuous(labels = scales::comma)+coord_cartesian(ylim = c(0, 1000)) 
3.	 The following codes was used  to Remove outliers in 'Profitability' 
Q1 <- quantile(df$Profitability, .25) 
Q3 <- quantile(df$Profitability, .75)
IQR <- IQR(df$Profitability) 
4. The following codes was used to: no_outliers <- subset(df, df$Profitability> (Q1 - 1.5*IQR) & df$Profitability< (Q3 + 1.5*IQR)) 
5.	The following codes was used dim(no_outliers)  
6.	The following codes was used to Remove outliers in 'Worldwide.Gross' 
Q1 <- quantile(no_outliers$Worldwide.Gross, .25) 
Q3 <- quantile(no_outliers$Worldwide.Gross, .75) 
IQR <- IQR(no_outliers$Worldwide.Gross) 
The following codes was used: df1 <- subset(no_outliers, no_outliers$Worldwide.Gross> (Q1 - 1.5*IQR) & no_outliers$Worldwide.Gross< (Q3 + 1.5*IQR)) 
The following codes was used  dim(df1)  
 
Step 3: Exploratory Data Analysis
1. The following codes was used to Summary Statistics/Univariate Analysis: 
summary(df1) 
2. The following codes was used to scatterplot:
ggplot(df1, aes(x=Lead.Studio, y=Rotten.Tomatoes..)) + geom_point()+ scale_y_continuous(labels = scales::comma)+coord_cartesian(ylim = c(0, 110))+theme(axis.text.x = element_text(angle = 90)) 
 The following codes was used bar chart:
ggplot(df1, aes(x=Year)) + geom_point() 
 
Step 4: Export data
1.	The following codes was used Export clean data:
write.csv(df1, “clean_df.csv")

Power B1
1.	IMPORT clean_df.csv file into power B1
 
2.	Transform data selected to view data.
 
3.	Power BI Dashboard that displays the following information listed below:
•	The average Rotten Tomatoes ratings of each genre
•	The number of movies produced per year 
•	The audience scores for each film  
•	The profitability per studio 
•	The worldwide gross per genre 


https://app.powerbi.com/groups/me/reports/b6d0c62e-066c-45f6-9cf2-de5113c094c0/ReportSection18551c692d3cf57db2ad



