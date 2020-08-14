# School District Analysis

## Project Overview

### Purpose

A school board has asked us to analyze data sets on students and schools within the district to create the following reports:

- A summary on the performance of each school in the district
- A summary identifying the top 5 performing schools based on overall passing rates
- A summary identifying the bottom 5 performing schools based on overall passing rates
- A summary for the average math score for each grade level from each school
- A summary for the average reading score for each grade level from each school
- A summary of scores by school spending per student
- A summary of scores by school size
- A summary of scores by school type

After creating these summaries, the board wanted us to re-calculate the aforementioned metrics as there was evidence of academic dishonesty in the reading and math grades for Thomas High School ninth graders. With this new information a new DataFrame was created displaying these scores as "Not a number" (NaN), and the summaries were re-calculated based on these assumptions.

### Resources

- Data Source: schools_complete.csv, students_complete.csv

### Results

Our analysis of the student and school data sets, accounting for academic dishonesty in math and reading from the 9th graders in Thomas High School, altered the district summary metrics in the following ways:

- All columns that measured population size - "Total Schools", "Total Students", and "Total Budget" remained unchanged. This is because rather than dropping rows of data for 9th graders at Thomas High School, we chose to instead alter their grades. The presence of these students feeds into our student_counts calculation which measures the count of students in the district based on ID's. Furthermore, there is no change to the Total Schools and Total Budget Column as there are independent from the scores of students in either area.

- Columns measuring averages for the math and reading scores were also left mostly unaffected. This is because the formulas that we use to calculate each score use the mean function on the math score column from our school_data_complete DataFrame. Since the new values for the 9th graders at Thomas High school are marked as NaN, the mean function does not include them and only reflects the averages of scores with a number value - so although they have no grades they are also not counted as part of the population when measuring average scores.

- Columns in the district summary pertaining to the percentage of students who passed each area separately or passed together were affected. This is because, as we mentioned, student population was unaffected but the absence of grades from 9th graders in Thomas High School takes away from the count of scores that is used as the numerator when calculating the averages for math and reading scores.

- District Summary with Thomas High School 9th grader grades:

- District Summary without Thomas High School 9th grader grades:

The School Summary was also affected by the absence of grades from 9th graders at Thomas High School.

- In the school summary, we again see that columns measuring population size, budget, and per student budget remain unchanged - for the same reasons mentioned previously (independence of variables in our calculations from reading and math scores). By showing that these totals remain unchanged, we can be sure that our formulas still counted the 9th graders at Thomas High school for per_capita calculations such as the "Per Student Budget" column while excluding their math and reading scores.

- Again in the school summary, we also see that there is hardly any difference made by the absence of the scores from the 9th graders at Thomas High School. This again demonstrates how our calculation of averages using the mean() function on math scores adjusts for the population of students at Thomas High School with a number value under their math or reading scores.

- Finally, our school summary demonstrates a more marked change in the percentage of students who passed math, reading, or both subjects. This again is due to the fact that our calculations for these columns take the now lowered count of students with grades above 70 (the predetermined passing grade) as the numerator while using the unchanged total count of students as the denominator when calculating percentage of passing students.

- District Summary with Thomas High School 9th grader grades:

- District Summary without Thomas High School 9th grader grades:

Replacing the ninth graders' math and reading scores affects the schools ranking due to the fact that school ranking is based on the "% Overall Passing" column. As has been pointed out, the percentage calculation under this column for Thomas High School shows a much lower percentage of students who passed both areas since the absence of grades for ninth graders leads to a smaller sum of students with passing grades while there is an unchanged student count.

- School rankings with Thomas High School 9th grader grades:

- School rankings without Thomas High School 9th grader grades:

Replacing the ninth grader scores resulted in a NaN value being reflected under math and reading scores by grade in each dataframe respectively:

Replacing the ninth grader scores lowered the values under the "% Passing Math", "% Passing Reading", and "% Overall Passing" columns for the "$630-645 Spending Ranges (Per Student" group as this is the bin that Thomas High School falls under:

Because Thomas High School falls under the "Medium" bin in our size_summary_df, replacing the ninth grade scores resulted in the following lowered values in the "% Passing Math", "% Passing Reading", and "% Overall Passing" columns:

Since Thomas High School is a Charter school, the values under the "% Passing Math", "% Passing Reading", and "% Overall Passing" columns in our type_summary_df were lowered as follows:

### Challenge Summary

After plugging in NaN's as the math and reading scores for the ninth graders in Thomas High School, there were some changes that occurred to some of our summaries. 

1. As mentioned in the results, all calculations dealing with the percentage of students that passed either area - math or reading - or both saw noticeable changes. This is because all formulas used in our DataFrames calculated the percentage of students based on a count of math/reading scores that exceeded the passing score of 70 and then measured that against a static calculation of total students. Since our formulas previously included passing float values for the 9th grader scores the percentages were higher; however by omitting these scores from the % passing calculations we can expect to see lowered passing percentages.

2. Thomas High School is now ranked lower when compared to other schools in the district. Since school rankings are based on overall passing percentages and we established that these percentages would be lowered by the absence of grades, the school fell significantly in ranking. From being ranked as the 2nd best overall to the 8th best after changing the 9th grader's scores.

3. Since Thomas High scool is classified as a Medium sized school, the negative changes in the percentage passing calculations carried over into the same columns for this bin in our school size dataframe. This negative change in performance not only affects the school but also impacts other schools that were categorized in the same bin based on school size.

4. The performance of Schools who spend $630-644 per student in our Scores by school spending summary was also negatively affected as a consequence of the lower passing percentages of Thomas High School. This is significant because prior to the change in scores this group of schools ($630-644) had a much higher passing math percentage, however after we made the alteration they are practically performing at the same level as the worst group of school in this subject.
