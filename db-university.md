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


## Departments
id:                                                           BIGINT PRIMARY KEY, UNIQUE, AUTO_INCREMENT, NOTNULL
name: (Dipartimento Ingegneria, Dipartimento Biologia...)     VARCHAR(100) NOTNULL, INDEX
city_venue:  (Napoli, Roma)                                   VARCHAR(50)  NULL
address_venue: (via barbagianni, 2)                           VARCHAR(50)  NULL

## Degree_course
id:                                                            BIGINT PRIMARY KEY, UNIQUE, AUTO_INCREMENT, NOTNULL
name: (Cdl Biologia della fecondazione, Ingegneria Biomedica)  VARCHAR(100) NOTNULL, INDEX
department_id:                                                 BIGINT     NOTNULL

## Courses
id:                                                            BIGINT PRIMARY KEY, UNIQUE, AUTO_INCREMENT, NOTNULL
name: (Biochimica, Genetica, Zoologia)                         VARCHAR(50)  NOTNULL, INDEX
exams: (Biochimica I, Biochimica II)                           VARCHAR(50)  NOTNULL, INDEX
credits: (CFU)                                                 SMALLINT     NULL
exam_appeal_id:                                                BIGINT       NOTNULL

## Teachers
id:                                                             BIGINT PRIMARY KEY, UNIQUE, AUTO_INCREMENT, NOTNULL
name: (teacher_name)                                            VARCHAR(50) NOTNULL, INDEX
lastname: (teacher_lastname)                                    VARCHAR(50) NOTNULL, INDEX
email: (teacher_email)                                          VARCHAR(50) NOTNULL
qualification: (type_of_teacher)                                VARCHAR(50) NOTNULL

## Examp_appeals
id:                                                             BIGINT PRIMARY KEY, UNIQUE, AUTO_INCREMENT, NOTNULL
exames_date: (date of exams)                                    DATE    NULL
student_grade:                                                  TINYINT     NULL
teacher_id                                                      BIGINT       NOTNULL
student_id                                                      BIGINT       NOTNULL

## Students
id:                                                              BIGINT PRIMARY KEY, UNIQUE, AUTO_INCREMENT, NOTNULL
name: (student_name)                                             VARCHAR(50) NOTNULL, INDEX
lastname: (student_lastname)                                     VARCHAR(50) NOTNULL, INDEX
university_code:                                                 VARCHAR(50) NOTNULL, INDEX
year_of_birth: (student_birth)                                   YEAR        NOTNULL
email: (student_email)                                           VARCHAR(50) NOTNULL
telephone_number: (student_telephone)                            SMALLINT    NULL
