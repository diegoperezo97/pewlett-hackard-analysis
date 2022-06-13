# MODULE 7: Employee Database with SQL

## Overview of the Analysis

Pewlett Hackard is a large company boasting several thousand employees and it's been around for a long time. As baby boomers begin to retire at a rapid rate Pewlett Hackard is looking toward the future in two ways. First, it's offering a retirement page for those who meet certain criteria. Second, it's starting to think about which positions will need to be filled in the near future. The number of upcoming retirements will leave thousands of job openings. What would happen to a company if they didn't look ahead and prepare for this many vacancies? It probably wouldn't be pretty.

Bobby is an up and coming HR Analyst whose task is to perform employee research. Specifically, he needs to find answers to the following questions:

1. Who will be retiring in the next few years
2. How many positions will Pewlett Hackard need to fill?

This analysis will help future-proof PewAt Hackard by generating a list of all employees
eligible for the retirement package. The employee data Bobby needs is the only available form of six CSV files because Pewlett Hackard has been mainly using Excel and VBA to work with their data. But now they've finally decided to update their methods and instead use SQL, a definite upgrade considering the amount of data.

### Purpose
* Help Bobby build an employee database with SQL by applying my data modeling, engineering, and analysis skills.

## Results of the Analysis

Deliverable 1:

1. 72,458 employees fall under the near-retirement criteria, which accounts for ~30% of the current workforce.
2. The most affected position will be senior “Senior Engineer”, which accounts for ~36% of the retiring workforce.

Deliverable 2:

1. 1,549 employees are eligible for the mentorship program
2. Most common positions for mentorship programs are “Staff” and “Senior Engineer”

## Summary of the Analysis

1. How many roles will need to be filled as the "silver tsunami" begins to make an impact? 

72,458 employees

SELECT COUNT(emp_no)
FROM (
SELECT DISTINCT ON (emp_no) emp_no FROM retirement_titles
WHERE to_date = ('9999-01-01')
) AS subquery;

2. Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?

According to Table 1. Number of employees per retiring employee, there are (on average) 1.4 employees for each new employee joining the company. In my opinion, this number seems low and as it may affect the “Business As Usual” of non-retiring employees, considering a person takes at least 30 days to start catching up.

**Table 1. Number of employees per retiring employees**
| TITLE | TOTAL EMPLOYEES | RETIRING EMPLOYEES | N EMP PER RETIRING
| ----------- | ----------- | ----------- | -----------
| Senior Engineer | 85,939 | 25,916 | 1.4
| Senior Staff | 82,024 | 24,926 | 1.4
| Engineer | 30,983 | 9,285 | 1.4
| Staff | 25,526 | 7,636 | 1.4
| Technique Leader | 12,055 | 1,090 | 1.4
| Assistant Engineer | 3,588 | 0.359375 | 1.4
| Manager | 9 | 2 | 1.3

SELECT title, COUNT(emp_no) FROM (
SELECT e.emp_no, e.first_name, e.last_name, t.title, t.from_date, t.to_date FROM employees AS e
INNER JOIN titles AS t
ON e.emp_no = t.emp_no
WHERE to_date = ('9999-01-01') ) AS subquery
GROUP BY title
ORDER BY count DESC;
