# Healthcare Database System

## Overview
This repository contains the design, implementation, testing, and deployment details for a healthcare database system. The system is designed to store and manage patient health information while ensuring data integrity, security, and accessibility.

## Requirements

### Functional Requirements
1. **Patient Information**: Capture and store essential details like name, date of birth, gender, contact details, and insurance information.
2. **Medical History**: Maintain records of diagnoses, allergies, medications, and treatments.
3. **Encounter Records**: Track patient encounters, including appointments, admissions, and discharges.
4. **Diagnostic Tests**: Store information on test types, results, and dates.
5. **Doctor Information**: Manage doctor profiles and their specialties.
6. **Prescriptions**: Maintain prescription data, including medication details, dosages, and dispensing records.
7. **Procedures and Surgeries**: Record details of medical procedures and surgeries performed.

### Non-Functional Requirements
- **Data Security**: Implement role-based access control and encryption for sensitive data.
- **Scalability**: Ensure the database can handle large datasets.
- **Performance**: Optimize queries for fast retrieval of patient and medical records.

## Entity-Relationship Diagram (ERD)
The ERD illustrates the relationships between entities such as `Patients`, `Doctors`, `MedicalHistory`, `EncounterRecords`, `DiagnosticTests`, `Prescriptions`, and `Procedures`.

*Attach the ER diagram here.*

## Database Design

### Schema Definitions
#### Patients Table
```sql
CREATE TABLE Patients (
    PatientID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100),
    DateOfBirth DATE,
    Gender ENUM('Male', 'Female', 'Other'),
    ContactDetails TEXT,
    InsuranceInfo TEXT
);
```

#### Doctors Table
```sql
CREATE TABLE Doctors (
    DoctorID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100),
    Specialty VARCHAR(100),
    ContactDetails TEXT
);
```

#### MedicalHistory Table
```sql
CREATE TABLE MedicalHistory (
    HistoryID INT AUTO_INCREMENT PRIMARY KEY,
    PatientID INT,
    Diagnosis TEXT,
    Allergies TEXT,
    Medications TEXT,
    FOREIGN KEY (PatientID) REFERENCES Patients(PatientID)
);
```

#### EncounterRecords Table
```sql
CREATE TABLE EncounterRecords (
    EncounterID INT AUTO_INCREMENT PRIMARY KEY,
    PatientID INT,
    DoctorID INT,
    Date DATE,
    Type ENUM('Appointment', 'Admission', 'Discharge'),
    FOREIGN KEY (PatientID) REFERENCES Patients(PatientID),
    FOREIGN KEY (DoctorID) REFERENCES Doctors(DoctorID)
);
```

#### DiagnosticTests Table
```sql
CREATE TABLE DiagnosticTests (
    TestID INT AUTO_INCREMENT PRIMARY KEY,
    PatientID INT,
    TestType VARCHAR(100),
    Result TEXT,
    TestDate DATE,
    FOREIGN KEY (PatientID) REFERENCES Patients(PatientID)
);
```

#### Prescriptions Table
```sql
CREATE TABLE Prescriptions (
    PrescriptionID INT AUTO_INCREMENT PRIMARY KEY,
    PatientID INT,
    DoctorID INT,
    Medication TEXT,
    Dosage TEXT,
    Date DATE,
    FOREIGN KEY (PatientID) REFERENCES Patients(PatientID),
    FOREIGN KEY (DoctorID) REFERENCES Doctors(DoctorID)
);
```

#### Procedures Table
```sql
CREATE TABLE Procedures (
    ProcedureID INT AUTO_INCREMENT PRIMARY KEY,
    PatientID INT,
    DoctorID INT,
    ProcedureName TEXT,
    ProcedureDate DATE,
    FOREIGN KEY (PatientID) REFERENCES Patients(PatientID),
    FOREIGN KEY (DoctorID) REFERENCES Doctors(DoctorID)
);
```

## Sample Data

### Patients Table
| PatientID | Name       | DateOfBirth | Gender | ContactDetails | InsuranceInfo |
|-----------|------------|-------------|--------|----------------|---------------|
| 1         | John Doe   | 1985-05-15  | Male   | (Encrypted)    | (Encrypted)   |
| 2         | Jane Smith | 1992-10-20  | Female | (Encrypted)    | (Encrypted)   |

*Similar data for other tables is included in the SQL script.*

## Testing and Validation

### Functional Testing
- Retrieve all patients with their medical history.
- Validate foreign key constraints by attempting invalid inserts.

### Security Testing
- Test role-based access control.
- Simulate SQL injection attempts to ensure queries are secure.

### Performance Testing
- Insert large datasets to evaluate query execution times.
- Optimize indexes for frequently used queries.

## Deployment

### Exporting Database
```bash
mysqldump -u root -p healthcare_db > healthcare_db_backup.sql
```

### Importing Database
```bash
mysql -u root -p healthcare_db < healthcare_db_backup.sql
```

## Future Enhancements
1. **Integration with Web Applications**: Develop a user-friendly interface for healthcare professionals.
2. **Advanced Analytics**: Add support for predictive analytics on patient data.
3. **Cloud Deployment**: Deploy the database to a cloud platform for scalability and availability.
4. **Mobile Access**: Enable mobile application support for real-time access to patient records.

## Conclusion
The healthcare database system is designed to meet the functional and security requirements for managing patient health information. It is scalable, secure, and optimized for real-world usage, ensuring reliable support for healthcare professionals.
