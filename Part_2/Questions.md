Part 19 — Your First Practice Set
Don't look for the answers immediately. Try them yourself.
Level 1
Q1. Display every student.
Q2. Display only student names.
Q3. Display names and CGPAs.
Q4. Find students from IT.
Q5. Find students with CGPA greater than 8.5.
Level 2
Q6. Display unique departments.
Q7. Display unique cities.
Q8. Find students whose name starts with A.
Q9. Find students whose name ends with a.
Q10. Find students whose name contains an.
Level 3
Q11. Sort students by CGPA from highest to lowest.
Q12. Sort students by age from lowest to highest.
Q13. Show the top 3 students by CGPA.
Q14. Show the top 3 IT students by CGPA.
Q15. Find CSE students with CGPA greater than 8.5, sorted from highest to lowest.
Level 4 — Think Like a SQL Developer
Q16.
Find the 5 highest-CGPA students from Bangalore.
Q17.
Find all students whose:
department = IT
AND
cgpa >= 8.5

and display only:
name
cgpa

Q18.
Find the unique departments represented by students whose CGPA is at least 8.5.
Q19.
Find students whose names start with A, sort them alphabetically, and return only 2.
Q20.
Find the top 3 students whose names contain the letter a.


Beginner
Q1. Count all students.
Q2. Find the average CGPA.
Q3. Find the highest CGPA.
Q4. Find the lowest CGPA.
Q5. Find the number of unique departments.
GROUP BY
Q6. Count students in each department.
Q7. Find the average CGPA of each department.
Q8. Find the maximum CGPA in each department.
Q9. Find the number of students in each city.
Q10. Find the average CGPA in each city.
HAVING
Q11. Show departments having more than 2 students.
Q12. Show departments whose average CGPA is greater than 8.5.
Q13. Show cities having at least 3 students.
NULL
Assume some city values are NULL.
Q14. Find students whose city is unknown.
Q15. Find students whose city is known.
Q16. Display Unknown whenever city is NULL.
CASE
Q17. Classify students:
CGPA >= 9       → Excellent
CGPA >= 8       → Good
otherwise       → Needs Improvement

Q18. Count how many students fall into each performance category.
Q19. For each department, count students with CGPA >= 9.
Q20. For each department, calculate:
department
student_count
average_cgpa
highest_cgpa
excellent_student_count

and only show departments with at least 2 students.
50. One Challenge Query
Try this without looking back:
For each department, consider only students whose CGPA is at least 8. Calculate the number of such students, their average CGPA, and how many have CGPA >= 9. Show only departments having at least 2 qualifying students, and sort by average CGPA from highest to lowest.

The structure should eventually come naturally:
SELECT
    department,
    COUNT(*) AS ...,
    AVG(...) AS ...,
    SUM(CASE WHEN ... THEN 1 ELSE 0 END) AS ...
FROM students
WHERE ...
GROUP BY department
HAVING ...
ORDER BY ... DESC;