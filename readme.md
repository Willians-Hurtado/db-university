
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
 
