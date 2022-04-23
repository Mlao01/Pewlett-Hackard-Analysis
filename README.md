# Pewlett-Hackard-Analysis

## Project Overview

>Now that Bobby has proven his SQL chops, his manager has given both of you two more assignments: determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program. Then, you’ll write a report that summarizes your analysis and helps prepare Bobby’s manager for the “silver tsunami” as many current employees reach retirement age.

** - Deliverable 1:** The Number of Retiring Employees by Title
** - Deliverable 2:** The Employees Eligible for the Mentorship Program
** - Deliverable 3:** A written report on the employee database analysis 

## Resources

**- Data Source:** 
    - departments.csv
    - dept_emp.csv
    - dept_manager.csv
    - employees.csv
    - salaries.csv
    - titles.csv

**- Software:** 
    - pgAdmin
    - PostgreSQL
    - VS Code

## Results:

- With the retirment_titles table we are able to see every eligible for retirement employee and how long they have worked at each position over the course of their career.

- The unique titles table that we created is showing the most recent title for employees who are about to retire.

![retiring_titles](/Resources/retiring_titles.PNG)

- The total number of staff who are about to retire equals to 72,458. Out of 72,458 retiring employees, 50,842 (%70.17) of those employees are in senior positions.

- Using the SQL below, we created a table for employees who are eligible for mentorship.

```
SELECT DISTINCT ON (e.emp_no) e.emp_no, e.first_name, e.last_name, e.birth_date, de.from_date, de.to_date, t.title
INTO mentorship_eligibility
FROM employees as e
	INNER JOIN dept_emp as de
		ON e.emp_no = de.emp_no
	INNER JOIN titles as t
		ON e.emp_no = t.emp_no
WHERE (t.to_date = '9999-01-01')
AND (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY e.emp_no ASC;
```

- Using the count keyword for SQL, we determined that there are only 1549 employees who are eligible for mentorship.

```
SELECT count(me.emp_no)
FROM mentorship_eligibility as me;
```

![mentorship_eligibility_count](/Resources/mentorship_eligibility_count.PNG)


## Summary

- Given that a large number of employees who are in senior position that are ready to retire, Pewlett-Hackard should ready to hire more to fill in the gap. 

- To lessen the impact of the retiring senior positions, Pewlett-Hackard should broaden the eligibility for the mentorship program. Currently, mentorship is only available for those who are born in 1965. To increase count of mentorship eligiblity, the range for birth date should be increase. Another option is to consider hiring date (how long they have been with the company) instead of birth date. 
