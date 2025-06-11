<!-- Selezionare tutti gli studenti nati nel 1990 (160)
Selezionare tutti i corsi che valgono più di 10 crediti (479)
Selezionare tutti gli studenti che hanno più di 30 anni
Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
Selezionare tutti i corsi di laurea magistrale (38)
Da quanti dipartimenti è composta l'università? (12)
Quanti sono gli insegnanti che non hanno un numero di telefono? (50) -->

Selezionare tutti gli studenti nati nel 1990 (160)

```sql
SELECT `name`, `surname`, `date_of_birth`
FROM `students`
WHERE `date_of_birth` BETWEEN "1990-01-01" AND "1990-12-31"
```

```sql
SELECT `name`, `surname`,`date_of_birth`
FROM `students`
WHERE `date_of_birth` >= "1990-01-01"
AND `date_of_birth` <= "1990-12-31";
```

Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
SELECT `id`, `cfu`
FROM `courses`
WHERE `cfu` > "10";
```

Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT `id`, `name`, `surname`
FROM `students`
WHERE `date_of_birth` < "1994-01-01";
```

```sql
SELECT `id`, `name`, `surname`
FROM `students`
WHERE YEAR(`date_of_birth`) < "1995";
```

Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)

```sql
SELECT *
FROM `courses`
WHERE `period` = "I semestre"
AND `year` = "1";
```

Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)

```sql
SELECT *
FROM `exams`
WHERE `hour` > "14:00:00"
AND `date` = "2020-06-20";
```

Selezionare tutti i corsi di laurea magistrale (38)

```sql
SELECT *
FROM `degrees`
WHERE `level` = "magistrale";
```

Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT COUNT(`id`)
FROM `departments`;
```

Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
SELECT COUNT(`id`)
FROM `teachers`
WHERE `phone` IS NULL;
```

<!-- Contare quanti iscritti ci sono stati ogni anno
Contare gli insegnanti che hanno l'ufficio nello stesso edificio
Calcolare la media dei voti di ogni appello d'esame
Contare quanti corsi di laurea ci sono per ogni dipartimento -->

Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT COUNT(`id`), `enrolment_date`
FROM `students`
WHERE YEAR(`enrolment_date`) =  "2018"
#OR YEAR(`enrolment_date`) =  "2019"
#AND YEAR(`enrolment_date`) =  "2020"
#AND YEAR(`enrolment_date`) =  "2021"
GROUP BY `enrolment_date`;
```

Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT COUNT(`id`), `office_address`
FROM `teachers`
GROUP BY `office_address`;
```

Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT `exam_id`, AVG(`vote`)
FROM `exam_student`
WHERE `exam_id` BETWEEN "1" AND "131"
GROUP BY `exam_id`;
```
