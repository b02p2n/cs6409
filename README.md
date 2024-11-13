java cCoursework 1: Student examples
The following examples are extracts from previous students' coursework to provide a guidance as to the standards expected. Full coursework
examples are not provided to avoid potential issues with copying (plagiarism); and also as the coursework changes each year so there is no
single coursework that matches the current.
These are examples of actual student work and not 'templates' to copy.
The coursework specifications vary each year, do not assume that the examples comply with the guidance in this year's specification.
Always refer to the current specification.
Start work early on your coursework and use the tutorials to gain formative feedback.
The 'good' examples are drawn from 2:1 or distinction responses, but marks are not provided.
The examples are accompanied by a brief comment to explain what was considered either "good" or "could be improved" about the given
example.
Past students have published their code with 'public' visibility on GitHub; you must not copy their code. Copying from other students, past or
present, is not appropriate even when correctly cited.
Section 1: Data exploration and preparation
Please note that last year this section was not separated into understanding and preparation in the same way as it is this year. The following
examples will give you an understanding of standard, but do not exactly match what you are asked to do this year.
General guidance
Describe and explain the steps you took, your findings, and any decisions you made.
For example, if you identify code quality issues then explain how you addressed these; or if you chose not to address them, then explain the
reason for not addressing them.
Do not focus on interpreting the data as if for a particular audience. For example, comments such as "I created _X_ chart to explore the range of
values of _Y_ variable and found that there were _Z_ outliers" are relevant in the context of this coursework; comments such as "The data shows
that more people migrated from in London in 2023 than in 2022." is not relevant in the context of this coursework.
Example 1: Boundary between High pass/Merit
Feedback: "The code shows some understanding of the use of pandas, though you could have done more to describe the data using the pandas
functions to show size, data types, ranges of values, etc. There is some attempt at adding structure in functions though it's a little jumbled. Try
and separate out the functions from the 'main' where you then call the functions."
It wasn't clear why the student commented out the code to create the charts.
The text supported the written code and evidenced that the student has gained a good understanding through applying the code, however the
code and explanation combined was not sufficient to attain a higher mark.
Student's code (parts removed to reduce the length of this page)
import pandas as pd
import matplotlib.pyplot as plt
if __name__ == '__main__':
 df = pd.read_csv('dataset.csv')
# first, lets translate all the data from german to english
 def ger_to_eng(dataframe):
 column_rename_map = {
 "StichtagDatJahr": "ReferenceYear", 
 "DatenstandCd": "Status",
 ...removed...
 
1/11
 }
 dataframe.rename(columns = column_rename_map, inplace = True)
 word_mapping = {
 'm?nnlich': 'male',
 'weiblich': 'female',
 '10- bis 19-J?hrige': '10-19 years old',
 ...removed...
# add more translations as needed
}
dataframe.replace(word_mapping, inplace=True)
# second, cleaning up the data
def del_redundant_cols(dataframe):
# i'll be removing columns which i deem redundant
del_columns = ['AgeGroupCode', 'DogAgeGroupLong', #'DogAgeGroupSort',
'GenderCode', 'DogGenderCode', 'BreedCode']
# delete specified columns
for col in del_columns:
del dataframe[col]
# next let's examine the data a bit
def dog_age_check(dataframe):
age_tally = dataframe['DogAgeGroupCode'].value_counts().sort_index()
age_tally = age_tally.drop(999, errors='ignore') # accounts for the unknown entries, which default to 999, removing them
# plotting a bar chart
plt.bar(age_tally.index, age_tally.values, color='skyblue')
plt.xlabel('Age')
 
2/11
plt.ylabel('Amount of Dogs')
plt.title('Age of Dogs Tabulated')
plt.show()
'''def owned_dog_count(dataframe):
# groupby OwnerID and sum up every number of dogs tied to that owner
dogs_per_person = dataframe.groupby('OwnerID')['NumberOfDogs'].sum().reset_index()
# Display the result
plt.figure(figsize=(10, 6))
dogs_per_person.plot(kind='bar', color='skyblue')
plt.title(f'')
plt.xlabel('Number of owned dogs')
plt.ylabel('Frequency')
plt.show()
plt.bar(dogs_per_person.index, dogs_per_person.values, color='skyblue')
plt.xlabel('Number of owned dogs')
plt.ylabel('Frequency')
plt.title('Number of dogs owned by a single person')
plt.show()
plt.figure(figsize=(10, 6))
plt.bar(dogs_per_person.index, dogs_per_person, color='skyblue')
plt.yscale('log') # Set y-axis to logarithmic scale
plt.title(f'Frequency Bar Graph for num_dog')
plt.xlabel("num of dogs")
plt.ylabel('Logarithmic Frequency')
plt.show()
def create_dog_bar_chart(dataframe):
owner_counts = dataframe.groupby('OwnerID')['NumberOfDogs'].nunique().reset_index()
# Plotting the bar chart
 
3/11
plt.bar(owner_counts['NumberOfDogs'], owner_counts['OwnerID'])
plt.xlabel('Number of Dogs Owned')
plt.ylabel('Number of Owners')
plt.title('Number of Owners for Each Number of Dogs Owned')
plt.show()'''
ger_to_eng(df)
del_redundant_cols(df)
dog_age_check(df)
df.to_csv('dataset_prepared.csv')
 
4/11
Example 2: Distinction
 
5/11
Feedback: "Great use of functions, comments and docstrings. Some great work on cleaning the data, especially considering how you would
detect outliers. Great visualisation of the data, what does this mean for your product??"
The code from the functions below has been removed, however the student went beyond what was taught in the course.
Code:
import math
import matplotlib.pyplot as plt
import pandas as pd
import warnings
from datetime import timedelta
warnings.simplefilter(action="ignore", category=FutureWarning)
# ignore the waring from df.approve
def print_general_statistics(df):
 """
 print the general information about the dataframe;
 print first 5 rows and all the columns of the data frame;
 demonstrate number of row and column of the data frame;
 print the data types; general statics information of the data frame
 Args:
 df: The data frame imported.
 """
 pd.set_option(
 "display.max_columns", None
 ) # set all the columns visible in the terminal printing
 pd.set_option("display.width", None)
 print("\nthe first 5 rows of dataframe :\n")
 print(df.head(12))
 print("\nThe Rows and Columns number:\n")
 print("\nRow Number :" + str(df.shape[0]))
 print("\nColumn Number :" + str(df.shape[1]))
 print("\nColumn data types:\n")
 print(df.dtypes)
 print("\nStatistics:\n")
 print(df.describe()) # Add your code inside the brackets
def null_data_detection(df):
def time_stamp_format_convert(df):
def breaking_point_detection(df):
def interpolation(df):
def timestamp_delete(df):
def outlier_detection(df, window_size=5, threshold=3):
def different_activity_frame_division(df):
def statics_histogram(df, name):
def statistics_boxplot(df, name):
def smoothing(df):
def smoothing_all(df):
if __name__ == '__main__':
 
 # read dataframe from csv
 df_ra代 写program、Java/Python
代做程序编程语言w = pd.read_csv("dataset.csv")
 # detect whether there is null data from the dataframe
 # print the general statistics
 print_general_statistics(df_raw)
 # detect null values
 df_after_null_preprocess = null_data_detection(df_raw)
 
6/11
 # convert timestamp to datetype and allow the after calculation
 df_after_time_stamp_convert = time_stamp_format_convert(df_after_null_preprocess)
 print_general_statistics(df_after_time_stamp_convert)
 # detect whether index =20928 has varied or not
 print(df_after_time_stamp_convert.loc[20928, "timestamp"])
 # delete same timestamp in the dataframe
 df_after_delete = timestamp_delete(df_after_time_stamp_convert)
 # interpolate lost data between the datapoints
 df_interpolation = interpolation(df_after_delete)
 # divide dataframe according to Activity
 df_activity_0, df_activity_1 = different_activity_frame_division(df_interpolation)
 # detect the outliers
 outlier_detection(df_activity_0)
 outlier_detection(df_activity_1)
 # draw the figures
 statics_histogram(df_activity_0, "Activity = 0")
 statics_histogram(df_activity_1, "Activity = 1")
 statistics_boxplot(df_activity_0, "Activity = 0")
 statistics_boxplot(df_activity_1, "Activity = 1")
 # smoothing the data frame
 df_final = smoothing_all(df_interpolation)
 df_final = df_final.drop(columns="timestamp_datetype")
 df_final.to_csv("output_file.csv", index=True)
Extract from the report:
This is just the first part so you can see the difference in the quality of the explanations. The student went on to explain the actions taken in each
of their functions, though some of the text was unnecessary as it also described the code which wasn't necessary.
 
7/11
Section 2: Database design and preparation
Please note that this section is substantially different in 2024.
Database design was included as part of the application design in coursework 2, and not coursework 1. The design of the database covered
requirements for their app, and not the data set so is different to what you are asked to do.
Students were not taught the first, second and third normal forms and so the expectations of their coursework was lower and therefore the
grades awarded higher than would be given for the same this year. I have tried to comment on the implications.
Preparation of the database is new to the coursework this year so there are no student examples from COMP0035. Students created the
database in COMP0034 and used different libraries. The students who achieved a higher grade showed originality in their code, tackled
databases with multiple tables, and provided well structured and documented code; those who achieved a high pass tended to just copy the
tutor's example code from the tutorial's and make minor changes to adapt it to their data.
Example 1: High pass
Feedback: "The ERD is a little confusing, why are you storing the account data in two places? The account data is enough. If you plan to create
the activity chart then you probably need a new table with attributes such as user_id, date/time, route they accessed. I assume the Visualisation
Chart is really the demograophic data so the table probably just needs a more meaningful name. A good attempt at each aspect of the design
with a few areas that could be improved."
Example 2: High Merit / Distinction boundary
Feedback given: "The ERD is well drawn and shows an understanding of normalisation. It is consistent with other aspects of the design."
Note that last year students were not taught 1NF, 2NF and 3NF, so this coursework evidenced that the student had carried out some
independent research to understand normalisation, though this is a copy and paste of the normalisation criteria rather than an explanation of
how these were applied in the context of this design.
Extract from student's PDF:
 
8/11
Example 3: Excellent (>70)
Feedback: "The development of the ERD similarly shows a clear grasp of the concepts of database design and normalisation and the resulting
design is well presented and approprate. This is an excellent coursework that not only evidences mastery of the techniques taught but also
clearly evidences an excellent grasp of the implications of the concepts and extensive additional reading."
This student provided a detailed explanation of the steps and decisions they made at each stage of normalisation, discussing the implications of
the choices they made. Their work evidenced that they understood and carefully applied the concepts. This far exceeded what was taught within
the course last year.
Student's ERD diagram only:
 
9/11
Section 3: Tools
Linting was not included in coursework 1 but was included in coursework 2. Source code control was assessed by looking at the commit history
and messages in their repository so cannot be included here. Including the environment files without seeing the students environment will not
give you a meaningful example. Since there is no meaningful way to provide student examples, the following is the feedback given to students
only.
Students achieving this highest marks in this section also provided evidence of the use of tools that went beyond the required tools. I will not list
these as this would then not be exceptional; this is an opportunity for students achieving the higher marks to research tools that support code
quality and development and apply something that is not covered in the course.
Source code control
High pass: "Some use of source code control over a period though you appear to mostly upload files rather than synchronise files between a
local and remote repository."
High merit: "Regular use of source code control with clear and meaningful commit messages."
Distinction: "Regular use of source code control with unique commit referencing. Evidence of effective use of branches and pull requests."
Linting
 
10/11
High pass: The code itself appeared free of issues that would typically be flagged by a linter so some assumption could be made as to effective
linting, but there was little or no evidence provided by the student to explain how they used linter tools to achieve this.
Merit: Provided evidence of using a linter, and the code appeared free of issues. Low merit: may have provided evidence of using the linter but
not then used this to improve the code.
Distinction: Provided evidence of using a linter at different stages; discussed actions taken and in cases where the issues could not be resolved,
gave an appropriate explanation for this. Some used more than one linter and compared the results.
Environment management
High pass: One or more of the required files was missing and/or in general the files were missing some details that prevented them from being
fully usable.
Merit: All files provided and were appropriate to allow the environment to be recreated and their code run. May have had minor issues e.g. a
package missing from requirements.txt, a detail within pyproject.toml missing or incorrect.
Distinction: Some students showed use of different techniques for creating and managing environments; and/or used the files with very specific
detail beyond the basics; and gave very clear guidance in the readme.md that led to the marker being able to successfully create an environment
and run the students code.
Last modified: Saturday, 28 September 2024, 6:36 PM
Previous activity
Data sets: ethics, data set size, collusion
Next activity ?
Examples of web apps from COMP0034
 
         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
