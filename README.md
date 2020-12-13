# Tuition-Cost-in-College-and-Analysis

  
## Abstract
The cost of college tuition has been one of the most important topics for both high school students and pre-college programs. It is necessary to have a data product that shows how tuition costs change between US universities. In our project, we want to perform research on the cost of college tuition based on several different categories such as in-state tuition vs out-state tuition; School type: public, private, and for profit. The dataset will also include degree length and state name so that we can plot a map view of the data product and compare cost by year. We added another dataset contains Date and Time data so we can plot a graph about Tuition Difference based on year. We will use different charts generated with R along with related R library and analyze the result. At the end of our project, we will come to a conclusion about tuition statistics for US colleges and make recommendations for high school students and pre-college students.


Motivation
------------------------------------------
The outstanding college student loan debt has reached an all-time high of $1.41 trillion in 2019, average $30,000 for each college students according to [**Figure 1** from U.S News report on student loan](https://www.usnews.com/education/best-colleges/paying-for-college/articles/see-how-student-loan-borrowing-has-risen-in-10-years), which demonstrated by the graph above showing 10 Years of average total student loan debt. There is no clear guideline application for pre-college student or transfer students to search state-wide college tuition data as an important reference before applying for U.S. College.   

The main motivation behind this project is to give a reference for them when they starting to apply for U.S. College, potentially avoid their regrets of endure high student loan debt after entered dreaming college for years. Our team wants to build an interactive application and report on U.S. college tuition which present clean and clear graphs and conclusion based on user's options such as Degree-length, School-Type, and In/Out-State.   

Secondary motivation in hindsight will hopefully be able to grab attention from United States Department of Education (ED) so that they can make some policies to slow down the increasing trend of college tuition fee and flat the curve of outstanding college student loan debt, which is definitely help a lot to the sustainable development of U.S. college.  

Related Applications 
------------------------------------------
There are several open source tables and application that related to our project. Thanks them for these data models, they provide some inspirations to our subtopic, like [**Figure 2** from U.S News report on Average College Tuition](https://www.usnews.com/education/best-colleges/paying-for-college/articles/paying-for-college-infographic), which show us a view of average college Tuition in 2020-2021. In [**EducationData**](https://educationdata.org/average-cost-of-college) website, we are able to view a list of table about average cost of college with analysis such as "why expensive?", "Cost by State", and "Room and Board On and Off Campus". More importantly, it has a nice work flow to discuss all the plots based on research which we can learn from it.  

The [**TuitionTracker**](https://www.tuitiontracker.org/) web application is powered by U.S. Department of Education data from IPEDS(Integrated Postsecondary Education Data System, a service provided by the National Center for Education Statistics). This interactive web tool shows what students really pay for college based on their family income with more than 3,800 colleges and universities in the United States.   

Another online application called [**CollegeTuitionCompare**](https://www.collegetuitioncompare.com/search/) provide a nice bar plot about in-state vs out-of-state tuition comparison. The application also include the graduation rates and diversity which help parents and students compare colleges using data that shows what schools actually cost the year student expect to enroll. They have highlighted the essential data such as financial aid and application stats so important data are transparent to users.  

Observations and Questions
------------------------------------------
From the existing web applications and tables, we find most of these data products having too much information even somewhat messy. The main problem is that they do not have options for users to choose what kind of information they want to view and compare so they just pop up a long form report including all the details.   

For example, it do give essential data such as Tuition difference between in-state and out-of-state, graduation rate, admission stats, and etc. However, it also include Not that important data such as student to faculty ratio, dormitory capacity, and average earning after 10 years of graduation with salary range.    

In our project, our analysis will focus on essential information for pre-college student and transfer student such as tuition difference between in-state and out-of-state, tuition increasing graph based on yearly report, and tuition difference between school type, and etc. In this way, our report will be more efficient and useful compared to the existing research based on U.S. college tuition.   

Our hypothesis is to explore which state has the most expensive tuition and which region has the most selective for pre-college student and college student to apply for college across the country. 

Preparing the Data 
------------------------------------------
Reshape original data to readable data set is a major part of this report. We spend a lot of time to extract data using several different functions of library and package in R.   

The data set originally comes from the US Department of Education. The most comprehensive and easily accessible data cames from TuitionTracker.org who allows for a .csv download! Unfortunately it's in a very wide format that is not ready for analysis, but tidyr R library can make quick work of that with pivot_longer().   

It has a massive amount of data, we have filtered it down to a few tables as seen in the attached .csv files. Tuition data can be quickly joined by dplyr::left_join(tuition_cost, diversity_school, by = c("name", "state")). Some of the other tables can also be joined but there may be some fuzzy matching needed.    

The Tuition and fees by college/university for 2018-2019, along with school type, degree length, state, in-state vs out-of-state from the Chronicle of Higher Education.    

The Historical averages from the National Center for Education Statistics (NCES) - spanning the years 1985 - 2016.    

Before we use this data set to explore the costs of college tuition in the US on their own, by geographic area, degree type, we have applied functions to reshape the data set. Here is the summary of the process:    

1. Drill in on the seemingly most popular regions using the "include" parameter in the plot_usmap() function. Regional divisions can be found in the doc of us_regdiv.pdf here.   

2. There were lots of missing data for room and board fee which will be added to total tuition fee in the end so we remove these rows when we want to compare these in-state tuition total and out-of-state tuition total.      

3. The original dataset do have a column to showing the states name. In order to simplify the output, we use merge anther column called Abbreviation to make room for the map view of US college tuition in state wise.    

4. Due to we use two different data set in this report, we only use couple columns in the history data set in order to not duplicate the information such as room and board, college name, state name are duplicated in these two data sets.   

5. Original history data set do not use typically academic year but in the format such as 2008-09 format, we change them to 20xx year format so that we can plot data year by year.    

6. In order to compare the tuition data in state wise, we have to calculate the average tuition for each state because there might have more than 50 college in one state but less than 10 college in another state.     

7. We have a docs for each columns field for these two data sets. In order to illustrate them to readers, we create a table for each columns names and descriptions for that to help understand.     

8. In order to zoom in the area of our findings, we use filter function to only display the corresponding information. For example, the highest tuition region we only display specific region instead of whole US map.  

9. Showing all the column names and explain each column to readers is hard but we use colnames function to get all column names first. Then we use cbind to append explanation and description. Finally, showing the table using kable function.   

R Library Foundations of the Project
------------------------------------------
This project may be imported into the RStudio environment and compiled by researchers wishing to reproduce this work for newest plot with future data sets, and having new findings or discussions from that.    

> The Core of Statistics were done using R 4.0.2 (R Core Team, 2020-06-22), the ggplot2 (v3.3.2; RStudio Team, 2020-06-19), and the knitr (v1.30; Yihui, 2020-09-22) packages.

For **ggplot2** package, this package has been used for creating graphics such as box plot, line plot, bar plot, and density plot from our reshaped data sets. With built-in theme, we are able to generate decent plots map variables to aesthetics with details to present in this report.      

From **knitr** package, this report is constructed to have reproducibility that it can regenerate the plot based on the latest dataset contains yearly report in the future. Using literate programming techniques for dynamic report generation in R.    

> The Initial Scenarios package is usmap 0.5.1 (Paolo Di Lorenzo, 2020-10-07).

For **usmap** package, we use plot_usmap(based on ggplot object) to plot state wise US map in convenient. The map data frames include Alaska and Hawaii conveniently placed to the bottom left, as they appear in most maps of the US. More over, it built-in function from U.S. Census Bureau help us to filter and divide the whole US map into four regions, which help us to zoom in specific area to analyze.     

> The Most Frequently Used package is dplyr (v1.0.2; RStudio Team, 2020-08-18).

For **dplyr** package, we use a lot of functions to reshape our data set and working with data frame through mutate, filter, arrange, group_by, summarize_all functions. Most of modification to the data set were using these functions list above.    

* **Note**: There are few functions has been used to reshape the data set in other packages. Due to limited usage, we will not list all these packages in this report such as melt function in reshape2 package; ggarange function in ggpubr package; readPNG function in png package. 




