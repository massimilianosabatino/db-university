
# EX - Query con SELECT

1. Selezionare tutti gli studenti nati nel 1990 (160)

    SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990;

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

    SELECT *
FROM `courses`
WHERE `cfu` > 10;

3. Selezionare tutti gli studenti che hanno più di 30 anni  

---TIMESTAMPDIFF TIENE IN CONSIDERAZIONE ANCHE MESE E GIORNO QUINDI POTEVA ESSERE SVOLTO CON:  
    SELECT TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) AS `eta`, `date_of_birth`, CURDATE() AS `oggi`  
FROM `students`  
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;  

----CALCOLO UNO  
    SELECT * FROM `students`  
WHERE YEAR(FROM_DAYS(datediff(curdate(), `date_of_birth`) + 1)) > 30;  
----/CALCOLO UNO  

----CALCOLO DUE  
    SELECT *
FROM `students`  
WHERE YEAR(CURRENT_DATE()) - YEAR(`date_of_birth`) > 30  
AND MONTH(CURRENT_DATE()) >= MONTH(`date_of_birth`)  
AND DAY(CURRENT_DATE()) >= DAY(`date_of_birth`);  
----/CALCOLO DUE  

----VECCHIO CALCOLO - RISULTATO UGUALE A PRIMO CALCOLO  
    SELECT *
FROM `students`
WHERE YEAR(FROM_DAYS(TO_DAYS(CURRENT_DATE()) - TO_DAYS(`date_of_birth`))) > 30;
----/VECCHIO CALCOLO  

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

    SELECT *
FROM `courses`
WHERE `period` = "I semestre" AND `year` = 1;

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

    SELECT *
FROM `exams`
WHERE `date` = "2020-06-20" AND HOUR(`hour`) >= 14;

6. Selezionare tutti i corsi di laurea magistrale (38)

    SELECT *
FROM `degrees`
WHERE `level` = "magistrale";

7. Da quanti dipartimenti è composta l'università? (12)

    SELECT COUNT(`id`) AS `dipartimenti`
FROM `departments`;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

    SELECT COUNT(`id`) AS `teachers_without_phone`
FROM `teachers`
WHERE `phone` IS NULL;
