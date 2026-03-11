# School Attendance Exploratory Data Analysis

## The Scenario

A senior leader preparing for coaching meetings with three school principals required an analysis of student attendance and absenteeism to guide data-informed decision-making. This project integrates multiple student-level datasets to create clean, reproducible analytical tables, enabling evaluation of attendance patterns and identification of opportunities for targeted intervention.

Three datasets were integrated:

- `Student Attendance.xlsx`: Records of student absences by type and total days absent.
- `Student Demographic.xlsx`: Student demographic information, including grade level and medical indicators.
- `Student Enrollment.xlsx`: Enrollment records identifying each student’s school and total days enrolled.

Because this analysis combines multiple datasets at different grains, a clear understanding of table relationships was critical. The diagram below illustrates the database schema and the aggregation strategy used to construct both student- and school-level datasets.

![[1A_database_design.png]]

## Definitions

- **Attendance Rate Goal:** Students are present for at least 95% of all days enrolled at a school.
- **Chronic Absenteeism Goal:** 17% or fewer students are chronically absent from school.
- **Chronic Absence** is a measure of how much school a student misses for any reason.
	- **Chronic:** Student missed 10% or more days enrolled for any reason.
	- **At-Risk:** Student missed 5 to 9% of days enrolled for any reason.
	- **Satisfactory:** Student missed less than 5% of days enrolled for any reason.

## Assumptions Made

- If a student record exists, then that student is currently enrolled at that school.
- The field `days_enrolled` reflects the number of days the student has been enrolled at this school since their first day at that school.

## Data Preparation, Cleaning, and Merging

The attendance, demographic, and enrollment datasets were imported and prepared in Python to construct clean, analysis-ready tables. The `pathlib` and `pandas` packages were used to programmatically access the raw data files, ensuring a reproducible workflow.

Data preparation steps included:

- Importing the three datasets into the notebook environment.
- Performing initial cleaning and validation, including handling missing values and edge cases such as records with zero absences.
- Merging datasets on `student_id` to create a comprehensive student-level dataset.
- Constructing derived metrics, including `percent_unexcused_absence`, and aggregating data to produce school-level summaries for comparative analysis.
- Constructing a school-level dataset for senior leadership to quickly refer to during their meeting.

## Analysis and Key Takeaways

To support leadership decision-making, interactive school- and student-level dashboards were developed in Tableau, enabling both system-wide evaluation and student-level intervention planning. Use the following link to explore the data: [[]]

### Attendance Performance

![[5A_school_attendance_rate.png]]
- All three schools fall below the district’s **95% attendance target**, indicating system-wide attendance challenges rather than an isolated school-level issue.

### Attendance Status Distribution

To better understand where these attendance gaps originate, student attendance status distributions were examined across schools.

![[5B_school_attendance_status_stacked_bar.png]]
- **North Star Middle** has the highest percentage of students with **Satisfactory attendance** (37.8% of students), but also has the highest percentage of students with **At-Risk attendance** (31.6% of students).
	- Because **North Star Middle** has the largest concentration of **At-Risk** students, targeted early interventions at this tier may produce the fastest improvement toward attendance goals.
- **Littlebrook Elementary** and **Stevenson High** face the highest rates of **Chronic absenteeism** (36.6% and 38.0%, respectively).
	- The elevated **Chronic absenteeism** rates at **Littlebrook Elementary** and **Stevenson High** suggest the need for sustained intervention strategies, including attendance monitoring, family outreach, and individualized support plans for students with persistent absence patterns.

### Drivers of Absenteeism

To understand the drivers behind absenteeism, the distribution of absence reasons was examined across all three schools.

![[5C_school_attendance_type_stacked_bar.png]]
- **Unexcused absences** are the biggest drivers of the lower attendance rate for **Littlebrook Elementary** (68.5% of absences) and **Stevenson High** (63.3% of absences).
	- This suggests that these schools should focus their intervention measures on family communication and establishing a strong attendance culture to prevent such absences.
- **Excused absences** (71.1% of absences) and **suspensions** (13.9% of absences) are the biggest drivers of lower attendance rate for **North Star Middle**.
	- This suggests that **North Star Middle** should focus their intervention on tightening processes around **excused absences** and evaluate their behavioral strategies to reduce student **suspensions**.

### Grade-Level Patterns

![[5D_littlebrook_attendance_grade_stacked_bar.png]]
- At **Littlebrook Elementary**, the kindergarten class faces the highest rate of **Chronic absenteeism**. Addressing this cohort early may support sustained attendance improvement over time.
- **Unexcused absence rate** tends to increase from kindergarten to 3rd grade. Leadership should look into sustained intervention strategies that target these absences to help ensure sustainable improved outcomes.
- 3rd through 5th grade, and 4th grade in particular, face a high rate of absences due to **suspensions** (13.8%, 28.8%, and 15.3%, respectively).
	- School leadership should examine behavioral strategies and intervention at these grade levels to ensure students are not unnecessarily absent from the classroom.

![[5E_northstar_attendance_grade_stacked_bar.png]]
- The 6th grade cohort faces the best rate of **Satisfactory attendance rate** (43.1%), but also the highest rate of **At-Risk Absenteeism** (36.1%).
	- Targeting this cohort will help create sustained improvements at **North Star Middle**.
- The rate of absences due to **suspensions** increases by grade level.
	- School leadership should address behavioral strategies to ensure disciplinary practices minimize lost instructional time while maintaining a supportive learning environment.

![[5E_stevenson_attendance_grade_stacked_bar.png]]
- **Chronic** and **At-Risk absenteeism** tends to increase across grade levels at **Stevenson High**.
	- Leadership should focus on sustained intervention strategies to help improve attendance outcomes moving foward.

## Conclusions

Across the three schools analyzed, attendance challenges appear systemic rather than isolated, with all schools falling below the district’s 95% attendance target. High concentrations of students near attendance risk thresholds indicate that small improvements among at-risk students could meaningfully improve overall attendance outcomes.

Unexcused absences emerged as the primary driver of reduced attendance rates at two schools, while excused absences and suspensions contributed more significantly at North Star Middle. These differences suggest that attendance challenges vary in nature across schools and require tailored intervention strategies rather than uniform solutions.

The analysis indicates that early intervention focused on at-risk students may provide the greatest opportunity for improvement before chronic absenteeism develops. Additionally, reviewing disciplinary practices and strengthening family communication strategies may reduce preventable absences.

The accompanying school- and student-level dashboards provide leadership with an ongoing decision-support tool, enabling both system-wide monitoring and targeted student intervention planning.

Because the dataset represents a cumulative snapshot rather than longitudinal attendance data, trends over time could not be evaluated. Future analyses incorporating time-series attendance records may provide deeper insight into seasonal patterns and intervention effectiveness.
