🏥 Hospital Management Database System

[![Academic Project](https://img.shields.io/badge/Academic%20Project-King%20Khalid%20University-blue)](https://www.kku.edu.sa)
[![Database](https://img.shields.io/badge/Database-Oracle%20%7C%20SQL-red)]()
[![Environment](https://img.shields.io/badge/Environment-SQL%20*Plus-orange)]()

[cite_start]A comprehensive Relational Database Management System (RDBMS) designed to streamline hospital operations[cite: 4]. [cite_start]The system securely stores, links, and facilitates seamless access to institutional records involving management, medical staff, patient workflows, room logistics, and automated financial billing[cite: 4, 12].

---

📖 Table of Contents
- [Project Overview](#-project-overview)
- [System Entities](#%EF%B8%8F-system-entities)
- [Database Schema & Architecture](#-database-schema--architecture)
- [Data Definition & Manipulation (DDL & DML)](#-data-definition--manipulation-ddl--dml)
- [Advanced SQL Analytics](#-advanced-sql-analytics)
- [Academic Context](#-academic-context)

---

🌟 Project Overview

[cite_start]Managing modern healthcare workflows demands centralized data tracking to eliminate logistical bottlenecks[cite: 4]. [cite_start]This project delivers a unified database structure containing **9 interconnected tables** that optimize clinical operations, staff accountability, and patient telemetry[cite: 5].

---

👁️ System Entities

[cite_start]The architecture models 9 distinct healthcare domains[cite: 5]:
1. [cite_start] Administration: Personnel responsible for structural control, execution monitoring, and performance evaluations[cite: 6, 13].
2. [cite_start] Stuff (Support Staff): General operational roles including secretaries, security, and cleaning staff[cite: 7, 13].
3. [cite_start] Doctors: Medical practitioners providing diagnoses and clinical monitoring[cite: 13].
4. [cite_start] Nurses: Registered care specialists monitoring patient recovery[cite: 13].
5. [cite_start] Patients: Incoming individuals receiving medical attention or treatments[cite: 13].
6. [cite_start] Reception (Reservations): Front-desk support handling entry workflows, schedule tracking, and user inquiries[cite: 8, 13, 14].
7. [cite_start] Departments: Clinical specializations grouping medical personnel and treatment scopes[cite: 9, 14].
8. [cite_start] Rooms: Accommodation management tracking room capacity, classes, and occupant constraints[cite: 11, 13].
9. [cite_start] Bills: Automated accounting pipelines computing total institutional service fees[cite: 12, 13].

---

🗄️ Database Schema & Architecture

[cite_start]The relationship ecosystem is defined through rigorous Relational Mapping (visualized in the document's "Entity-Relationship (ER) Diagram")[cite: 16].

Core Relational Infrastructure:
[cite_start] `STUFF` Table:  Primary key `Stuff_id`, storing metadata regarding job titles, salaries, and shift work-hours[cite: 15].
[cite_start] `DOCTOR` Table: Primary key `Doctor_id`, logging specializations, medical experiences, and university credentials[cite: 17].
[cite_start] `NURES` Table: Primary key `Nurse_id`, managing healthcare delivery support metrics[cite: 19].
[cite_start] `ADMINISTRATION` Table: Primary key `Administration_id`[cite: 22]. It maps operational management to the medical corps via foreign keys: `doctor_id`, `Nurse_id`, and `Stuff_id`[cite: 22].
[cite_start] `PATIENTS` Table: Primary key `Patient_id`, directly referenced by clinical personnel and allocation assets (`room_no`)[cite: 38].
[cite_start] `RESPCAON` (Reception/Reservation) Table: Primary key `Reservation_no`, tracking timestamps (`Date_entry`, `Date_exit`) and complaints linked to incoming patient registries[cite: 46].
[cite_start] `DEPARTMENT` Table: Primary key `Dept_id`, bundling fields to coordinate spatial locations with doctors and patients[cite: 56].
[cite_start] `ROOM` Table: Primary key `room_no`, utilizing tracking metrics for availability statuses (e.g., 'reserved', 'empty', 'Full of')[cite: 78, 79, 80].
[cite_start] `BILL` Table: Primary key `bill_no`, tracking metrics including `days_no` to auto-calculate transaction fees against active foreign keys[cite: 85].

---

💻 Data Definition & Manipulation (DDL & DML)

[cite_start]The repository provides production-ready Oracle SQL scripts encompassing detailed constraints (`PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`)[cite: 22, 38, 64].

Table Creation Blueprint Example (`ADMINISTRATION`):
```sql
CREATE TABLE administration (
    Administrat_id NUMBER(4) PRIMARY KEY,
    Name VARCHAR(30),
    Age NUMBER(2),
    Gender VARCHAR(10),
    Address VARCHAR(30),
    Phone_no NUMBER(10) NOT NULL,
    Salary NUMBER(6) NOT NULL,
    Work_hour NUMBER(2),
    Email VARCHAR(30),
    Nationat VARCHAR(30),
    Status VARCHAR(10),
    Gradua_uni VARCHAR(30),
    doctor_id NUMBER(4) NOT NULL,
    Nurse_id NUMBER(4) NOT NULL,
    Stuff_id NUMBER(4) NOT NULL
);

-- Integrity Constraints Setup
ALTER TABLE administration ADD CONSTRAINT fk_nu FOREIGN KEY (Nurse_id) REFERENCES Nures(Nurse_id);
ALTER TABLE administration ADD CONSTRAINT fk_st FOREIGN KEY (Stuff_id) REFERENCES stuff(Stuff_id);
ALTER TABLE administration ADD CONSTRAINT fk_do FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id);
