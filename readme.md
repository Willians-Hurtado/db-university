
## table name: department
- id - (BIGINIT) - primary key - auto_increment - (NOT NULL)
- name - VARCHAR(255) - (NOT NULL)

## table name: degree program
- id - (BIGINIT) - primary key - auto_increment - (NOT NULL)
- department_id - (NOT NULL)
- name - VARCHAR(255) - (NOT NULL)

## table name: course
- id - (BIGINIT) - primary key - auto_increment - (NOT NULL)
- name - VARCHAR(255) - (NOT NULL)
- degreeprogram_id - VARCHAR(255) - (NOT NULL)

## table name: teacher
- id - (BIGINIT) - primary key - auto_increment - (NOT NULL)
- name - VARCHAR(255) - (NOT NULL)
- lastname - VARCHAR(255) - (NOT NULL)
- course_id - VARCHAR(255) - (NOT NULL)

## table name: student
- id - (BIGINIT) - primary key - auto_increment - (NOT NULL)
- name - VARCHAR(255) - (NOT NULL)
- lastname - VARCHAR(255) - (NOT NULL)
- admission_date - DATE - (NOT NULL)
- exame_id - VARCHAR(255) - (NOT NULL)


## table name: exam
- id - (BIGINIT) - primary key - auto_increment - (NOT NULL)
- course_id - VARCHAR(255) - (NOT NULL)
- type - VARCHAR(255) - (NOT NULL)
- date - DATE
 



## consegna
1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)



## soluzione

1. SELECT `date_of_birth`
FROM `students`
WHERE YEAR (`date_of_birth`) = '1990'

2. SELECT `cfu`
FROM `courses`
WHERE `cfu` > '10'

3. SELECT `date_of_birth`
FROM `students`
WHERE YEAR (`date_of_birth`) < '1995'

4. SELECT `year`, `period`
FROM `courses`
WHERE `year`= 1 AND `period` = 'I semestre' 

5. SELECT `date`,`hour`
FROM `exams`
WHERE `date` = '2020/06/20' AND `hour` > '14:00'

6. SELECT `name`
FROM `degrees`
WHERE `name` LIKE '%Magistrale%'

7. SELECT `name`
FROM `departments`

8. SELECT `phone`
FROM `teachers`
WHERE `phone` IS null




## Consegna 
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)



## Soluzione
1. 
SELECT students.id, students.name AS 'student_name', students.surname, degrees.name AS 'degree_name'
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'

2. 
SELECT degrees.*
FROM `courses`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`department_id` = 7
AND `degrees`.`level` = 'Magistrale'

3. 
SELECT courses.id, courses.name AS 'course_name', teachers.id, teachers.name AS 'teacher_name', teachers.surname
FROM course_teacher
JOIN courses ON course_teacher.course_id = courses.id
JOIN teachers ON course_teacher.teacher_id = teachers.id
WHERE teachers.id = 44

4. 
SELECT students.id, students.surname, students.name AS 'student_name', degrees.name AS 'degree_name', departments.name AS 'department_name'
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.surname, students.name ASC

5. 
SELECT degrees.id AS 'degree_id', degrees.name AS 'degree_name', courses.id AS 'course_id', courses.name AS 'course_name', teachers.id AS 'teacher_id', teachers.name AS 'teacher_name', teachers.surname 
FROM course_teacher
JOIN courses ON course_teacher.course_id = courses.id
JOIN degrees ON courses.degree_id = degrees.id
JOIN teachers ON course_teacher.teacher_id = teachers.id
ORDER BY degrees.id 

6. 
SELECT DISTINCT departments.name, teachers.name, teachers.surname
FROM course_teacher
JOIN courses ON course_teacher.course_id = courses.id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
JOIN teachers ON course_teacher.teacher_id = teachers.id
WHERE departments.name = 'Dipartimento di Matematica'




## GROUP BY
1. Contare quanti iscritti ci sono stati ogni anno

SELECT YEAR (students.enrolment_date) AS year, COUNT(*) AS number_of_students
FROM students
GROUP BY year
ORDER BY year  

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT teachers.office_address AS adress, COUNT(*) AS number_of_office
FROM teachers
GROUP BY adress
ORDER BY adress  

3. Calcolare la media dei voti di ogni appello d'esame

SELECT exam_student.exam_id AS exam, AVG(exam_student.vote) AS grade_average
FROM exam_student
GROUP BY exam
ORDER BY exam 

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT departments.name AS department, COUNT(degrees.id)  AS number_of_degrees
FROM degrees
JOIN departments ON degrees.department_id = departments.id
GROUP BY department
ORDER BY department