# cs440-pj4

## Project description

In this project, you will analyze a similar data set as project 3 using PySpark but with some
different tasks. You could only use PySpark DataFrame or RDD API. You will get zero point if
you use SQL queries, or other Python libraries like pandas. You must not write full SQL queries
in lieu of the [DataFrame API](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/dataframe.html). That is, you must not use functions like `sql()`.

## Project setup

Installing PySpark is easy. You just do 
```bash
pip install pyspark
``` 
as you would normally install other Python packages.
We will run a Python version of `3.10` to grade your project. You are only allowed to use `PySpark` apart from the standard library of Python.

## Data Description

> Note: This section is exactly the same as project3. Feel free to skip it if you like

In this project, you will analyze a [data set](https://drive.google.com/file/d/1D0MUXh6SPT7sPLl-xoNm_zyPEvujmOAH/view?usp=sharing) of of NYC yellow taxi data within a certain period.
There are 19 columns in the csv file. Some of the important columns are:

| Column | Description |
| ---| --- |
| tpep_pickup_datetime | The date and time of the pickup. |
| tpep_dropoff_datetime | The date and time of the dropoff. |
| Passenger_count | The number of passengers in the vehicle. |
| Trip_distance | The elapsed trip distance. |
| PULocationID | TLC Taxi Zone of the pickup. |
| DOLocationID | TLC Taxi Zone of the dropoff. |

## Your Task

In this project, you will implement four PySpark tasks.

> Note: For all four tasks below, we only consider trip distance strictly greater than 2 miles. That is, the first step of all the four tasks is to filter the trips.

### Task 1

Compute the total distance of all rides grouped by PULocationID *(equivalent to group and aggregate in SQL)*. The output of your result CSV should have the following format (The number is just for illustration purpose). Sum all the distance using raw value and round to two decimal points in the result CSV file (Read: The result trip distance should have exactly two digits after the decimal point). Rank the line by the ascending order of the numerical value of `PULocationID`. Put your Python code in a file called `main1.py`.

#### Sample Output

1,100.00
<br />
2,100.00
<br />
...

#### Command

We will run your program using the following command (we grade the code in Linux):

```bash
./main1.py {input_data} {output_directory}
```

The `input data` (i.e., first argument of the command line) is the input data file your Python program should read from. The `output directory` (i.e., second argument of the command line) is the name of the output directory your Python program should write to. You should not hard code these two file or directory’s name. Rather, you should read it from the command line.

For example, `./main1.py data.csv output1` means your Python program should read the data from `data.csv` and output the result to `output1`. If you have a result dataframe df, you could use the function 
```python3
df.write.csv(sys.argv[2])
````
to output the result.

### Task 2

Locate the Top 10 most active location ID and output it in the descending order of the activeness.<br/>
An ID’s activeness is defined by the total number of drop off and pickup. In case of a tie, the lower
locationID comes first.<br/>
The output of your result CSV should have the following format (The number is just for illustration purpose). Put your Python code in a file called `main2.py`.

#### Sample Output

1
<br />
2
<br />
...

#### Command

We use a command similar to the [first task](#command), except that we now use `main2.py`.

### Task 3

List the top 3 days of the week with the largest number of daily average pick-ups and output it in the descending of the average pick-ups. Calculate the average pick-ups by taking an average of different dates falling in the same day of the weeks. For example, if you want to find the average pick-ups on Monday, you first find all the dates which are Monday. Then, you take an average of pick-ups of all those dates. In case of a tie, the lower day comes first (e.g., if there is a tie, Monday comes before Tuesday).<br/>
The output of your result CSV should have the following format (The number is just for illustration purpose). Put your Python code in a file called `main3.py`. Write the day in full
name (e.g., **Wednesday** not *Wed*)

#### Sample Output

Monday
<br />
Thursday
<br />
...

#### Command

We use a command similar to the [first task](#command), except that we now use `main3.py`.

### Task 4

For each hour of a day (00 to 23) — in the order from 00 to 23, find the zone in the Brooklyn borough with the largest number of total pick-ups (in case of a tie, pick the zone with the smallest alphabetical order). The map between location ID and borough, (and zone) could be found [here](https://drive.google.com/file/d/10MesoJtAl8bnF15awlrgs4Mjlb1HdnSs/view?usp=share_link).<br/>
> Again, this is just a sample file. We may use different files for grading. So you should not hard code anything.

The output of your result CSV should have the following format (The number is just for illustration purpose). Put your Python code in a file called `main4.py`.

#### Sample Output

00,Bay Bridge
<br />
01,Bay Bridge
<br />
...

#### Command

We will run your program using the following command (we grade the code in Linux):
```bash
./main4.py {input_data} {map_data} {output_directory}
```
The `input_data` (i.e., first argument of the command line) is the input data file your Python
program should read from. The `map_data` (i.e., second argument of the command line) records
the relationship between locationID, borough, and zone. The `output_directory` (i.e., third
argument of the command line) is the name of the output directory (CSV) your Python program should write to. You should not hard code these files’ name. Rather, you should read it from the command line. Use the function similar to [task 1](#command) for output.

For example, `./main4.py data.csv map.csv output4` means your Python program should
read the data from `data.csv` and output the result to `output4`. The map information is in the file
`map.csv`.


## Grading

Each task is of 25% of the total grade of this project. We will compare your result CSV file with our result CSV file. If the two files are the same, you get full credit for this task, otherwise you get partial credits based on your result CSV file. We may use a different test data set, so you should not hard code anything (We will not change the schema though).

## Deliverable

Put 4 python file into a single zip file with your Purdue career account as the file name and upload it into the Gradescope. We understand that Gradescope does not accept zip file. Just leave it as what Gradescope will give you, or you could upload 4 single Python files separately. You zip file should have the following structure (using a career account called `wang0000`):
```
wang0000.zip
-- main1.py
-- main2.py
-- main3.py
-- main4.py
```
