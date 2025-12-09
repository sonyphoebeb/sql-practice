# 🧾 Patient Schema & Table Creation (09-12-2025)

## 📌 Overview

This document contains the SQL script used to create the **_patient_** schema and the **patient.details** table.  
It includes fields for basic patient information along with metadata such as creation and modification tracking.

## 🛠️ SQL Script


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
