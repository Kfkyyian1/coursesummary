# Using R to combine CSV files into a table & uploading to MySQL 
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/9bbaf743-7d38-45d0-973f-30c764c10ffb) <br>
<p>After loading in the necessary package, a function named “uploadCSV” was used to read in all the CSV files and combining it into a table as instructed in the question. </p>

<p>The database details and folder path were first established. Then the list.files command was used to list out all the files that are in CSV format within the specified folder. This function is used instead of listing out all 4 file names, so that it’ll be more sustainable in the future when there’s new CSV files being added to the folder.  </p>

Moving on, all the CSV files were then combined into a dataframe called combined_data, breakdown of the command below:
- lapply(csv_files, read.csv, header = TRUE) <br>
-- Within list apply, the function reads each file within the csv_files vector that stores all the csv files, including the header. <br>
-- One dataframe is created for each CSV file.<br>
- do.call(rbind,…) <br>
-- do.call is a function that takes a function (in this case, rbind, which binds rows together) and a list of arguments to be passed to that function. <br>
-- In this command, do.call applies the rbind function to the list of dataframes obtained from the previous step. <br>
-- rbind combines these dataframes by stacking them vertically and merging them into a single dataframe. <br>
-- All the separate dataframes from each CSV file will be combined into a single dataframe called combined_data. <br>
<p>The connection to the MySQL database was opened, so that a table called “course_status” created with the data from combined_data can be imported into MySQL. Lastly, the connection was closed. </p>

# Data Cleaning & Sanity Check in MySQL
1. Check if the rows and columns match the raw data <br>
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/df0c7eb8-9621-465c-a74e-4870976d7706) <br>
<img width="452" alt="image" src="https://github.com/Kfkyyian1/coursesummary/assets/146427900/221b14dd-b50f-4b34-9f38-3b24129b6763"> <br>

2. Remove the additional column <br>
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/3810a8b0-ed1e-457c-979d-e87f265d837f) <br>
<img width="440" alt="image" src="https://github.com/Kfkyyian1/coursesummary/assets/146427900/a5818063-55d1-41c9-9091-d57f5fe51769">

3. Check type of data <br>
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/1d150fbf-a00a-4c51-9964-8d80e0f62ba8) <br>
<img width="225" alt="image" src="https://github.com/Kfkyyian1/coursesummary/assets/146427900/4aa7a81e-c964-4272-9518-e06e9921ee36">

4. Clean up column names <br>
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/2d5a6cd5-9090-43e2-b0a0-80eaff4caa55) <br>
<img width="452" alt="image" src="https://github.com/Kfkyyian1/coursesummary/assets/146427900/3e28cd5e-d1c9-439b-9df2-2ef715299859">

# Create a new table containing (i) the number of courses ever offered, (ii) percentage of active courses offered, (iii) percentage of retired courses for each program and school <br>
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/65b43504-f60b-42e2-bac2-e1e49e24ed5c) <br>
After refreshing MySQL, the table is created as shown below. <br>
<img width="1310" alt="image" src="https://github.com/Kfkyyian1/coursesummary/assets/146427900/57332529-0dd9-4f1f-8495-60b2a163c891"> <br>

# Visualise data in R
1. Read in course_summary table into R <br>
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/51b7929b-dcd2-43b7-9ce7-27783337bd5d) <br>
<img width="628" alt="course_summary_in_R" src="https://github.com/Kfkyyian1/coursesummary/assets/146427900/33bcde8d-4cf3-4f88-9729-bddaa3832559"> <br>

2. Data Sanity Check <br>
- The number of rows and columns match the table in MySQL, indicating all the data has been fetched. (93 rows, 5 columns) <br>
- The structure of the data was checked using the str command. The data type observed is correct and ready for plotting. <br>
![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/6246e9e4-b9a8-4b13-9a35-c61a71f94308)

3. Visualisation
![Total Number of Active   Retired Courses](https://github.com/Kfkyyian1/coursesummary/assets/146427900/caa55806-d75f-4d81-8e75-57f95e709e73) <br>
<p>The senior management team is often constrained by time, and only requires a quick overview of the data. Therefore, the visualisation is simplified to only showcase the total number of active and retired courses within each school. Notably, the School of Science & Technology exhibits the number of active courses, surpassing retired courses. In contrast, other schools demonstrate a lower number of active courses in comparison to their retired courses. School of Humanities have the lowest total number of courses. </p>

With the visualisation above, the senior management team can analyze and possibly take some of the next steps below and make informed decisions:
- Explore programs in School of Science & Technology, investigate factors that contribute to the high number of ongoing courses.
- Assess the demand for humanities and business-related courses, explore opportunities to enhance program offerings.
- Optimize resource allocation based on ongoing courses.

![image](https://github.com/Kfkyyian1/coursesummary/assets/146427900/bde7bd23-91ea-48b7-af2d-05ea0ca4864d)






