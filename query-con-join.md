# EX - Query con JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia  

    SELECT `students`.*, `degrees`.`name` AS `degrees_name`  
FROM `students`  
JOIN `degrees`  
ON `degree_id` = `degrees`.`id`  
WHERE `degrees`.`name` = "Corso di Laurea in Economia";  


2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze  

    SELECT `degrees`.*, `departments`.`name`  
FROM `degrees`  
JOIN `departments`  
ON `department_id` = `departments`.`id`  
WHERE `departments`.`name` = "Dipartimento di Neuroscienze"  
AND `level` = "Magistrale";  

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)  

    SELECT `courses`.`name`, `courses`.`description`, `courses`.`period`  
FROM `course_teacher`  
JOIN `courses`  
ON `course_id` = `courses`.`id`  
WHERE `teacher_id` = 44  
ORDER BY `courses`.`period`;  

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il
relativo dipartimento, in ordine alfabetico per cognome e nome  

SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `degrees`.`website`, `departments`.`name` AS `department_name`  
FROM `students`  
JOIN `degrees`  
ON `degree_id` = `degrees`.`id`  
JOIN `departments`  
ON `degrees`.`department_id` = `departments`.`id`  
ORDER BY `surname`, `students`.`name`;  

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti  

SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`  
FROM `degrees`  
JOIN `courses`  
ON `degrees`.`id` = `courses`.`degree_id`  
JOIN `course_teacher`  
ON `courses`.`id` = `course_teacher`.`course_id`  
JOIN `teachers`  
ON `course_teacher`.`teacher_id` = `teachers`.`id`  
ORDER BY `degree_name`, `teacher_surname`, `teacher_name`;  

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)  

SELECT DISTINCT `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `departments`.`name`  
FROM `teachers`  
JOIN `course_teacher`  
ON `teachers`.`id` = `course_teacher`.`teacher_id`  
JOIN `courses`  
ON `course_teacher`.`course_id` = `courses`.`id`  
JOIN `degrees`  
ON `courses`.`degree_id` = `degrees`.`id`  
JOIN `departments`  
ON `degrees`.`department_id` = `departments`.`id`  
WHERE `departments`.`name` = "Dipartimento di Matematica"    
ORDER BY `teacher_surname` ASC, `teacher_name` ASC;  

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami  