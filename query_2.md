## Group by

# 1 Contare quanti iscritti ci sono stati ogni anno

    SELECT COUNT(`id`), YEAR(`enrolment_date`) 
    FROM `students` 
    GROUP BY YEAR(`enrolment_date`);  
# 2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio

    SELECT COUNT(`id`), `office_address` 
    FROM `teachers` 
    GROUP BY `office_address`;

# 3 Calcolare la media dei voti di ogni appello d'esame

    SELECT AVG(`vote`) 
    FROM `exam_student`;

# 4 Contare quanti corsi di laurea ci sono per ogni dipartimento

    SELECT COUNT(`id`), `department_id` 
    FROM `degrees` 
    GROUP BY `department_id`;

## Joins

# 1 Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

    SELECT `students`.* 
    FROM `degrees` INNER JOIN `students` 
    ON `students`.`degree_id` = `degrees`.`id` 
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia';    

# 2 Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

    SELECT * 
    FROM `departments` 
    INNER JOIN `degrees` 
    ON `degrees`.`department_id` = `departments`.`id` 
    WHERE `degrees`.`level` = 'magistrale' AND `departments`.`name` = 'Dipartimento di Neuroscienze';

# 3 Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

    SELECT * 
    FROM `course_teacher` 
    INNER JOIN `courses` 
    ON `course_teacher`.`course_id` = `courses`.`id` 
    WHERE `course_teacher`.`teacher_id` = 44;

# 4 Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

    SELECT `students`.`name`, `students`.`surname`, `degrees`.* 
    FROM `students` 
    LEFT JOIN `degrees` 
    ON `students`.`degree_id` = `degrees`.`id` 
    ORDER BY `students`.`surname`;

# 5 Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

    SELECT `degrees`.`name`, `courses`.`name`, `teachers`.`name`, `teachers`.`surname` 
    FROM `degrees` 
    LEFT JOIN `courses` 
    ON `courses`.`degree_id` = `degrees`.`id` 
    LEFT JOIN `course_teacher` 
    ON `course_teacher`.`course_id` = `courses`.`id` 
    LEFT JOIN `teachers` 
    ON `course_teacher`.`teacher_id` = `teachers`.`id`;

# 6 Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

# 7 BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente filtrare i tentativi con voto minimo 18.