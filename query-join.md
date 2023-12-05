Group
1. Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(*) AS `student_count`, YEAR(`enrolment_date`)
FROM `students`
GROUP BY YEAR(`enrolment_date`);

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(*) AS `teachers_count`, `office_address`
FROM `teachers`
GROUP BY `office_address`;

3. Calcolare la media dei voti di ogni appello d'esame
SELECT COUNT(`exam_id`) AS `exams_count`, AVG(`vote`) AS `average_vote` 
FROM `exam_student` 
GROUP BY `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(*) AS `degrees_count`, `department_id`
FROM `degrees`
GROUP BY `department_id`;

Join
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name` AS `degree_name`
FROM `students`
JOIN `degrees` ON `degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
SELECT `degrees`.`name`, `degrees`.`level`, `departments`.`name` AS `department_name`
FROM `degrees`
JOIN `departments` ON `department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
FROM `course_teacher`
JOIN `courses` ON `course_id` = `courses`.`id`
JOIN `teachers` ON `teacher_id` = `teachers`.`id`
WHERE `teacher_id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` AS `degree_name`, `degrees`.`level` AS `degree_level`, `departments`.`name` AS `department_name`
FROM `students`
JOIN `degrees` ON `degree_id` = `degrees`.`id`
JOIN `departments` ON `department_id` = `departments`.`id`
ORDER BY `students`.`name`, `students`.`surname` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.