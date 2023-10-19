# PostGIS Workshop

## Veri Tabanında Gerekli Olan Tabloları Oluşturma:

```
-- Öğrenci Tablosu
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100)
);

-- Dersler Tablosu
CREATE TABLE courses (
    course_id SERIAL PRIMARY KEY,
    course_name VARCHAR(100),
    instructor VARCHAR(100)
);

-- Kayıtlar Tablosu
CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INTEGER REFERENCES students(student_id),
    course_id INTEGER REFERENCES courses(course_id),
    enrollment_date DATE
);
```

## Verileri Ekleme

```

-- Öğrenci verilerini eklemek için
INSERT INTO students (first_name, last_name, email)
VALUES 
  ('Ahmet', 'Yılmaz', 'ahmet.yilmaz@example.com'),
  ('Mehmet', 'Demir', 'mehmet.demir@example.com'),
  ('Ayşe', 'Kaya', 'ayse.kaya@example.com'),
  -- Diğer öğrencileri eklemek için aynı formatta devam edebilirsiniz.
  ('Fatma', 'Şahin', 'fatma.sahin@example.com');


-- Ders verilerini eklemek için
INSERT INTO courses (course_name, instructor)
VALUES 
  ('Matematik 1', 'Prof. A'),
  ('Fizik 1', 'Prof. B'),
  ('Kimya 1', 'Prof. C'),
  -- Diğer dersleri eklemek için aynı formatta devam edebilirsiniz.
  ('Biyoloji 1', 'Prof. D');


-- Kayıt verilerini eklemek için
INSERT INTO enrollments (student_id, course_id, enrollment_date)
VALUES 
  (1, 1, '2023-09-15'),
  (2, 2, '2023-09-16'),
  (3, 1, '2023-09-17'),
  (4, 2, '2023-09-18');

```


-- Tüm öğrencileri listele:
```
SELECT * FROM students;
```

-- Bir öğrencinin adını ve soyadını al:

SELECT first_name, last_name FROM students WHERE student_id = 1;

-- Bir dersin adını ve eğitmenini al:

SELECT course_name, instructor FROM courses WHERE course_id = 101;

-- Bir öğrencinin aldığı dersleri listele:

SELECT students.first_name, students.last_name, courses.course_name
FROM students
INNER JOIN enrollments ON students.student_id = enrollments.student_id
INNER JOIN courses ON enrollments.course_id = courses.course_id
WHERE students.student_id = 1;

-- Bir dersin kaç öğrenci tarafından alındığını say:

SELECT course_id, COUNT(*) AS student_count
FROM enrollments
WHERE course_id = 101
GROUP BY course_id;


-- Bir öğrencinin bir dersi alıp almadığını kontrol et:

SELECT course_id, COUNT(*) AS student_count
FROM enrollments
WHERE course_id = 101
GROUP BY course_id;

-- Yeni bir öğrenci ekle:

INSERT INTO students (first_name, last_name, email)
VALUES ('Ali', 'Demir', 'ali.demir@example.com');

-- Yeni bir ders ekle:

INSERT INTO courses (course_name, instructor)
VALUES ('Tarih 1', 'Prof. E');

-- Bir öğrenciyi ir derse kaydet:

INSERT INTO enrollments (student_id, course_id, enrollment_date)
VALUES (5, 103, '2023-09-19');

-- Bir öğrencinin ders kaydını güncelle:

UPDATE enrollments
SET course_id = 102
WHERE student_id = 5 AND course_id = 103;

-- Bir öğrencinin ders kaydını sil:

DELETE FROM enrollments
WHERE student_id = 5 AND course_id = 102;

```


