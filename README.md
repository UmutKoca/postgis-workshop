# PostGIS Workshop
Hkmo İstanbul Şubesi'nde verilen Postgis eğitiminin kodlarını içerir.

# Veri Tabanında Gerekli Olan Tabloları Oluşturma:

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
