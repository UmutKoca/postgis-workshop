# PostGIS Workshop
Hkmo İstanbul Şubesi'nde verilen Postgis eğitiminin kodlarını içerir.

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
