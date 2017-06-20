HARD MODE:

1) Create a report for a student that shows what classes (s)he has left to take based on the major enrolled. So for example, if the major requires classes U, V, W, X, Y, and Z, and the student has enrolled in U, X, and Y, the remaining classes to be taken are V, W, and Z. You can assume if a student enrolled in a class that they student completed the class with a passing grade.

  SELECT concat(last_name, ', ', first_name) AS student_name, major_name, concat(class_subject, ' - ', class_nbr) as class_name FROM student
  JOIN major
  ON student.major_id = major.major_id
  JOIN major_class
  ON major.major_id = major_class.major_id
  JOIN class
  ON major_class.class_id = class.class_id
  WHERE class.class_id NOT IN (

  SELECT student_class.class_id FROM student_class
  WHERE student_class.student_id = student.student_id AND
  completion_flag != 1

  );
