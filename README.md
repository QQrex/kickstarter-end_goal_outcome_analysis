# **kickstarter-end_goal_outcome_analysis**

## **Purpose**

Louise's kickstarter campaign for her play, Fever, is close to meet her fundraising goal amount.
She would like to know how her current campaign fares when compared to other campaigns.

## **Overview of Project**

Using the kickstarter Excel dataset she provided to us, we will:
1. Look at sucessful, failed and canceled outcomes based on launch dates in parent category theater
2. Look at sucessful, failed and canceled percentages rates based on amount goals in subcategory plays

## **Analysis and Challenges**


**[Date Conversion]**

At first glance of the excel dataset, we see the deadline/launch at dates were given to us in unix epoch time.
We simply use the formula *((epoch timestamp/60)/60/24)+DATE(1970,1,1)* to convert to MM/DD/YYYY.
Next, when we perform our analysis, we would like to filter our date by year.
To do this we simply use the formula *=Year(MM/DD/YY)* in excel to seperate out the years from the dates.


![Date conversion from unix timestamp to readable timestamp and year](https://user-images.githubusercontent.com/96326293/147867720-56bc3331-c17b-411e-9afa-efb5717d74d3.PNG)
>Column I and L = original unix timestamp, Column J and M = readable timestamp, and Column K and N = Years



**[Outcomes based on Launch Date]**

Since Louise's kickstarter campaign is a play, we would want to sort the data to look only at Parent Category Theater and Years
The easiest way to accomplish this is to create a pivot table from the dataset and set:
  1. filters (in this order) = Partent Category Theater and years
  2. Rows = launched at (date)
  3. Columns = outcomes
  4. Values = Count of outcomes

![Pivot table of outcomes based on launch date](https://user-images.githubusercontent.com/96326293/147867996-54f0f40d-ca8d-4117-a565-25581b555243.PNG)
>Pivot table of outcomes based on launch dates


**[Outcomes based on Goals Chart]**

The goal amounts of all the kickstart Plays varies in amount.
In order for us to perform our analysis, we should create a dollar-amount range.
Once our range has been decided we will need to sort our goal amounts vs. count of sussessful, failed or canceled campaigns.
Now that we have what we need to do planned out we need to excute:
1. Create a new Excel sheet named "outcomes plays goal chat"
2. Fill Row 1 with headers Goal, Number of Sucessful, Number of failed, Number Canceled, % Sucessful, % Failed, % Canceled, and % Sum (check if % sum = 100)
3. Fill Column "A" with our range, Sum, and Check (use to check sum against orignal dataset)
4. Count our goal amounts in each range by using the function *=Countif()*
   
   -For our starting range we use =COUNTIFS(Plays!$F:$F, "**x**",Plays!$D:$D, "<1000")
   
   -For our middle range we use =COUNTIFS(Plays!$F:$F, "**x**",Plays!$D:$D, ">=**Lbound**",Plays!$D:$D, "<=**Ubound**")
   
   -For our ending range we use =COUNTIFS(Plays!$F:$F,"**x**",Plays!$D:$D,">=50000")
   
   >**x** = "succesful", "failed" or "canceled" and **Lbound** is lower range and **Ubound** is higher range

6. Sum succesful, failed and canceled counts in "Sum" row
7. Check each category using =COUNTIFS(Plays!$F:$F,"**x**",Plays!$D:$D,">=0") in "Check" row
8. Calculate count of total projects for each range row
9. Calculate % for each range using function *=ROUND(B2/$E2*100,1)* and sum % for each range row to check if = to 100

Our final table:

![Outcome based on Goals table](https://user-images.githubusercontent.com/96326293/147869541-ed8ff9d6-78e1-457d-bd55-6483f1faba4a.PNG)


## **Results**

**[Outcomes based on Launch Dates]**
![Theather_Outcomes_vs_launch](https://user-images.githubusercontent.com/96326293/147626344-76b76c4d-d59a-4282-946a-f1562cb36215.png)
>line chart of months versus count of sussessful, failed and canceled theater campaigns

From the graph above, we see a large increase in successful campaigns in the months of May, June and July. This increase peaks at May and declines through June and July.
Also from the graph above, we don't see a significant uptrend in the amount of failed campaigns throughout the months.


**[Outcomes based on Goals]**
![Outcomes_vs_Goals](https://user-images.githubusercontent.com/96326293/147630396-48a227d5-8cf6-41cf-80fd-82f1534a38f7.png)
>the graph above shows % of successful, failed and canceled based on different goal amounts from theater-plays campaigns

From the graph above we see the most successful percentage (72% to 75%) were from goal amounts set at less than 1000 to 4999. 
There is also a noticable increase in succesful percentage (66%) from goal amounts set at 35000 to 44999.
With that said, most campaigns with 5000 or more saw failure rates 50% or higher.

**[Limitations]**


Looking at the % outcomes based on goal amounts we can see see two distinct uptrends, one at at the lower range and one toward the higher range. The increase in % towards the higher range is due to the low amount of plays with such high goal amounts. These could mean there may be outliers in our dataset. We can perform a box and whisker plot for each outcome to see if outliers excist in our data. Also, we can create another table/line chart looking at % outcomes vs all plays instead of total plays for each range to see overall success rate of each range.
