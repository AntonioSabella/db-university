<!--
Descrizione: 
Modellizzare la struttura di una tabella per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..);
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. 

-->

# University


## table: Departments  (model:Department)
- id:                                                           BIGINT PRIMARY KEY, UNIQUE, UNSIGNED, AUTO_INCREMENT, NOTNULL
- name: (Dipartimento Ingegneria, Dipartimento Biologia...)     VARCHAR(100) NOTNULL, INDEX
- city_venue:  (Napoli, Roma)                                   VARCHAR(50)  NULL
- website:   (department-website)                               VARCHAR(255)  NOTNULL
- language:  (language)                                         DEFAULT(it-IT) NOTNULL
- address_venue: (via barbagianni, 2)                           VARCHAR(50)  NULL
- email :                                                       VARCHAR(50) NOTNULL
- head_of_department:                                           VARCHAR(100) NOTNULL

## table: Degree_courses  (model:Degree_course)
- id:                                                            BIGINT PRIMARY KEY, UNIQUE, UNSIGNED, AUTO_INCREMENT, NOTNULL
- name: (Cdl Biologia della fecondazione, Ingegneria Biomedica)  VARCHAR(100) NOTNULL, INDEX
- degree_description:                                            MEDIUMTEXT   NULL
- department_id:                                                 BIGINT       NOTNULL
- level:                                                         VARCHAR(50) NOTNULL
- email:                                                         VARCHAR(50) NOTNULL
- website:                                                       VARCHAR(100) NOTNULL
## table: Courses  (model:Course)
- id:                                                            BIGINT PRIMARY KEY, UNIQUE, UNSIGNED, AUTO_INCREMENT, NOTNULL 
- name: (Biochimica, Genetica, Zoologia)                         VARCHAR(50)  NOTNULL, INDEX
- description:                                                   MEDIUMTEXT   NULL
- year:                                                          YEAR         NOTNULL
- period:                                                        VARCHAR(50)  NOTNULL
- exams_modules: (Biochimica I, Biochimica II)                   VARCHAR(50)  NOTNULL, INDEX
- description: (course description)                              MEDIUMTEXT   NULL
- credits: (CFU)                                                 TINYINT      NULL
- degree_courses_id:                                             BIGINT  NOTNULL

## table: Teachers  (model:Teacher)
- id:                                                             BIGINT PRIMARY KEY, UNIQUE, UNSIGNED, AUTO_INCREMENT, NOTNULL
- name: (teacher_name)                                            VARCHAR(50) NOTNULL, INDEX
- lastname: (teacher_lastname)                                    VARCHAR(50) NOTNULL, INDEX
- phone_number:                                                   VARCHAR(20) NULL  
- email: (teacher_email)                                          VARCHAR(50) NOTNULL
- qualification: (type_of_teacher)                                VARCHAR(50) NOTNULL
                                                 

<!-- Tabella ponte -->
______________________________
### pivot table: course_teacher
- course_id:                                                   BIGINT      NOTNULL
- teacher_id:                                                   BIGINT      NOTNULL



_______________________________

## table: Exam_appeals  (model:Exam_appeal)
- id:                                                             BIGINT PRIMARY KEY, UNIQUE, UNSIGNED, AUTO_INCREMENT, NOTNULL
- exam_date: (date of exams)                                     DATE    NULL
- exam_hour:                                                     TIME   NOTNULL
- location:                                                      VARCHAR(50) NOTNULL
- address:                                                       VARCHAR(50) NOTNULL
- exam_note: (notes about exams)                                 TEXT    NULL
- student_grade:                                                  TINYINT NULL
- course_id :                                                    BIGINT  NOTNULL
- student_id :                                                    BIGINT  NOTNULL

## table: Students  (model:Student)
- id:                                                             BIGINT PRIMARY KEY, UNIQUE, UNSIGNED, AUTO_INCREMENT, NOTNULL
- degree_courses_id: 
- name: (student_name)                                             VARCHAR(50) NOTNULL, INDEX
- lastname: (student_lastname)                                     VARCHAR(50) NOTNULL, INDEX
- university_code:                                                 VARCHAR(50) NOTNULL, INDEX, UNIQUE, AUTO_INCREMENT
- year_of_birth: (student_birth)                                   DATE        NOTNULL
- year_of_subscription: (university_subscription)                  DATE        NOTNULL
- email: (student_email)                                           VARCHAR(50) NOTNULL
- telephone_number: (student_telephone)                            SMALLINT    NULL
- student_credits: (CFU)                                           SMALLINT    NULL
- exams_done:                                                      TINYINT     NULL
- exams_to_do:                                                     TINYINT NULL

_________________________________
## pivot table: exam_student
- exam_id
- student_id
<!-- eventualmente il voto potrebbe essere una voce della tabella pivot, ma è stato sconsigliato come approccio. Risulta meglio inserire una tabella ulteriore come quella sottostante -->

_______________________________

## table: Votes (model: Vote)
- id:                           BIGINT PRIMARY KEY, UNIQUE, UNSIGNED, AUTO_INCREMENT, NOTNULL
- student_id
- exam_id
- vote:                          TINYINT    NULL                              