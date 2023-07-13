# pandas-challenge

##  Overview
In this assignment we were provided with two .csv files that contained standardized test results and school details
for a school district. We were also provided a notebook with starter code to work through and create multiple data frames.
We are to analyze the data frames we created and find two observable trends in the data.

This readme will cover a few places where I struggled with my code and how I was able to overcome those roadblocks.

### School Summary
- The first thing I did was group the data by school using the .groupby() function, the starter code did not have a cell for this so I added a new one

*data_by_school = school_data_complete.groupby(["school_name"])*

- I used the .first() method to pull the first value for "type" column for each unique school.

  *school_types = data_by_school["type"].first()*

  https://pandas.pydata.org/docs/reference/api/pandas.core.groupby.DataFrameGroupBy.first.html

### Highest-Performing Schools and Bottom Performing Schools
- I used the .sort_values() method to sort my 'per_school_summary' dataframe base on the "Overall Passing Rate (%)" column.

  https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html

  *top_schools = per_school_summary.sort_values(["Overall Passing Rate (%)"], ascending=False)* for the top schools
  *bottom_schools = per_school_summary.sort_values(["Overall Passing Rate (%)"], ascending=True)* for the bottom schools

### Math/Reading Scores by Grade
- I struggled to find the correct syntax in this section. I knew I had to use the .groupby() method, I worked with an agent on the AskBCS channel
 and they guided me to the right syntax. It is important to pay attention to your brackets and parenthesis.

*ninth_grade_math_scores = ninth_graders.groupby(["school_name"])["math_score"].mean()*

### Scores by School Spending
- In this section I once again had to work with an AskBCS agent to get my code to run. I used the pd.cut method as we covered in section 4.3 of class. I was trying to reference
  *school_spending_df["Per Student Budget"]* but was receiving data type errors. Finally we agreed on just referencing *per_school_capita* and that got rid of the errors.

*school_spending_df["Spending Ranges (Per Student)"] = pd.cut(per_school_capita, spending_bins, labels = labels, right=False)*


## Analysis

-Charter schools have a higher overall passing rate by a wide margin over district schools. If we look at the 'Scores by School Type' section we can see that 'charter' schools
show a 90.4(%) passing rate against 'district schools' 53.6(%).

-By studying the 'Scores by School Spending' section we can reach the conclusion that higher spending does not equate to higher test scores. The schools in the highest tier of
spending '645-680' have the lowest overall passing rate at 53.5(%). As the per capita spending decreases scores steadily increase all the way to 90.3(%) for schools spending
less than 585 per student.

