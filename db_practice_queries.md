# 🧾 Patient Schema & Table Creation

## 📌 Overview

This document contains the SQL script used to create the **_patient_** schema and the **patient.details** table.  
It includes fields for basic patient information along with metadata such as creation and modification tracking.

## 🛠️ SQL Script

```sql
CREATE SCHEMA patient;

GO

CREATE TABLE patient.details (
    id INT IDENTITY(1,1) PRIMARY KEY,
    guid UNIQUEIDENTIFIER DEFAULT NEWID(),
    patient_first_name VARCHAR(250),
    patient_last_name VARCHAR(250),
    patient_age DATE,
    is_deleted BIT DEFAULT 0,
    created_by VARCHAR(50) DEFAULT (SUSER_SNAME()),
    created_at DATETIME DEFAULT (GETDATE()),
    modified_by VARCHAR(50),
    modified_at DATETIME
);
📂 Table Structure
Column Name	Data Type	Description
id	INT (IDENTITY)	Primary key (auto-increment)
guid	UNIQUEIDENTIFIER	Unique global identifier
patient_first_name	VARCHAR(250)	Patient's first name
patient_last_name	VARCHAR(250)	Patient's last name
patient_age	DATE	Date of birth or age reference
is_deleted	BIT	Soft delete flag (0 = active, 1 = deleted)
created_by	VARCHAR(50)	User who created the record
created_at	DATETIME	Timestamp when record was created
modified_by	VARCHAR(50)	User who last modified the record
modified_at	DATETIME	Timestamp of last modification

✨ Notes
Uses NEWID() to auto-generate GUID.

Tracks record creation and modification using system functions.

Supports soft deletion using is_deleted flag.
