# 🧾 Patient Schema & Table Creation (09-12-2025)

## 📌 Overview

This document contains the SQL script used to create the **_patient_** schema and the **patient.details** table.  
It includes fields for basic patient information along with metadata such as creation and modification tracking.

## 🛠️ SQL Script


    CREATE SCHEMA patient;

    GO
    
    CREATE TABLE patient.patient (
        id INT IDENTITY(1,1) PRIMARY KEY,
        guid UNIQUEIDENTIFIER DEFAULT NEWID(),
        first_name VARCHAR(250) NOT NULL,
        last_name VARCHAR(250) NOT NULL,
        middle_name VARCHAR(250),               
        date_of_birth DATE,
        gender CHAR(1) CHECK (gender IN ('M','F','O')), 
        blood_group VARCHAR(3),                 
        contact_number VARCHAR(20),
        email VARCHAR(100),
        address_line1 VARCHAR(250),
        address_line2 VARCHAR(250),
        city VARCHAR(100),
        state VARCHAR(100),
        country VARCHAR(100),
        postal_code VARCHAR(20),
        is_deleted BIT DEFAULT 0,
        created_by VARCHAR(50) DEFAULT (SUSER_SNAME()),
        created_at DATETIME DEFAULT (GETDATE()),
        modified_by VARCHAR(50),
        modified_at DATETIME
    );

## 📂 Table Structure

<table>
  <tr>
    <th>Column Name</th>
    <th>Data Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>INT (IDENTITY)</td>
    <td>Primary key (auto-increment)</td>
  </tr>
  <tr>
    <td>guid</td>
    <td>UNIQUEIDENTIFIER</td>
    <td>Unique global identifier</td>
  </tr>
  <tr>
    <td>patient_first_name</td>
    <td>VARCHAR(250)</td>
    <td>Patient's first name</td>
  </tr>
  <tr>
    <td>patient_last_name</td>
    <td>VARCHAR(250)</td>
    <td>Patient's last name</td>
  </tr>
  <tr>
    <td>patient_age</td>
    <td>DATE</td>
    <td>Date of birth or age reference</td>
  </tr>
  <tr>
    <td>is_deleted</td>
    <td>BIT</td>
    <td>Soft delete flag (0 = active, 1 = deleted)</td>
  </tr>
  <tr>
    <td>created_by</td>
    <td>VARCHAR(50)</td>
    <td>User who created the record</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>DATETIME</td>
    <td>Timestamp when record was created</td>
  </tr>
  <tr>
    <td>modified_by</td>
    <td>VARCHAR(50)</td>
    <td>User who last modified the record</td>
  </tr>
  <tr>
    <td>modified_at</td>
    <td>DATETIME</td>
    <td>Timestamp of last modification</td>
  </tr>
</table>

## ✨ Notes

* Uses NEWID() to auto-generate GUID.
* Tracks record creation and modification using system functions.
* Supports soft deletion using is_deleted flag.

## 🧾 Sample Data for `patient.patient` Table

    INSERT INTO patient.patient 
    (first_name, last_name, middle_name, date_of_birth, gender, blood_group, contact_number, email,
     address_line1, address_line2, city, state, country, postal_code)
     
    VALUES
    ('Aarav', 'Sharma', 'Raj', '1990-02-15', 'M', 'B+', '+91-9876543210', 'aarav.sharma@gmail.com',
     '12 MG Road', 'Apt 101', 'Mumbai', 'Maharashtra', 'India', '400001'),
    
    ('Ananya', 'Verma', NULL, '1995-08-20', 'F', 'O+', '+91-9123456789', 'ananya.verma@outlook.com',
     '45 Park Street', NULL, 'Delhi', 'Delhi', 'India', '110001'),
    
    ('Rohan', 'Patel', 'Kumar', '1988-11-05', 'M', 'A-', '+91-9988776655', 'rohan.patel@yahoo.com',
     '78 Lotus Lane', 'Block B', 'Ahmedabad', 'Gujarat', 'India', '380001'),
    
    ('Sanya', 'Rao', 'Priya', '2000-06-30', 'F', 'AB+', '+91-9871122334', 'sanya.rao@gmail.com',
     '23 Flower Street', NULL, 'Bangalore', 'Karnataka', 'India', '560001'),
    
    ('Vivaan', 'Singh', NULL, '1985-12-12', 'M', 'O-', '+91-9811223344', 'vivaan.singh@outlook.com',
     '56 Green Avenue', 'Suite 5', 'Chennai', 'Tamil Nadu', 'India', '600001');

## 📝 View All Records

    SELECT * FROM [patient].[patient];

