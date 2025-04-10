
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
