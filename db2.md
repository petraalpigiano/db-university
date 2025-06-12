<!-- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18. -->

Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT
`students`.`id` "student_id",
`students`.`degree_id`,
`students`.`name`,
`students`.`surname`,

`degrees`.`name` AS "degree_name",
`degrees`.`level`
FROM `students`
INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";
```

Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze

```sql
SELECT
`degrees`.`id`"degree_id",
`degrees`.`department_id`,
`degrees`.`name`"degree_name",
`degrees`.`level`,

`departments`.`name`"department_name"

FROM `degrees`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = "magistrale"
AND `departments`.`name` = "Dipartimento di Neuroscienze";
```

Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT
`course_teacher`.`teacher_id`,
`course_teacher`.`course_id`,

 `courses`.`name`"course_name",

`teachers`.`name`,
`teachers`.`surname`

FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id`= `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `courses`.`id`= `course_teacher`.`course_id`
WHERE `teachers`.`id` = 44;
```

Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome

```sql
SELECT
`students`.`id` "student_id",
`students`.`name` "student_name",
`students`.`surname` "student_surname",
`students`.`degree_id`,

`degrees`.`name` "degree_name",
`degrees`.`department_id`,

`departments`.`name` "department_name"

FROM `students`
INNER JOIN  `degrees`
ON `students`.`degree_id`= `degrees`.`id`
INNER JOIN  `departments`
ON `degrees`.`department_id`= `departments`.`id`
ORDER BY `student_name`, `student_surname`;
```

Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT
`degrees`. *,

`courses`.id "course_id",
`courses`.name "course_name",

`teachers`.id "teacher_id",
`teachers`.name "teacher_name",
`teachers`.surname "teacher_surname"

FROM `degrees`
INNER JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.teacher_id = `teachers`.id;
```

Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

```sql
SELECT DISTINCT
`teachers`.id "teacher_id",
`teachers`.`name` "teacher_name",
`teachers`.surname "teacher_surname"

FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.id = `course_teacher`.teacher_id
INNER JOIN `courses`
ON `courses`.id = `course_teacher`.course_id
INNER JOIN `degrees`
ON `courses`.degree_id = `degrees`.id
INNER JOIN `departments`
ON `degrees`.department_id = `departments`.id
WHERE `departments`.`name` = "Dipartimento di Matematica"
#GROUP BY `teachers`.id, `teachers`.`name` ,`teachers`.surname
ORDER BY `teachers`.`id`
```
