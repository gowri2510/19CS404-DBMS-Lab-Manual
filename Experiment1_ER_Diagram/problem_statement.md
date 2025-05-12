# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Student Name

## Scenario Chosen:
Hospital 

## ER Diagram:
![image](https://github.com/user-attachments/assets/1afe56d6-a2dc-4de1-b984-d4424b1f2fee)


## Entities and Attributes:
Billing : date, method, billing id, total amount, paayment status.
Hospital : contact, city, special list, name.
Medical records : id, prescribed medications, test result, treatment, diagnosis.
Doctor : doctor id, doctor name, specialization, hospital contact, work shedule.
Patient : id, full name, DOB, Gender, address, phone no. ...

## Relationships and Constraints:
Relationship1 (Billing, Hospital) It is a Many-to-One Relationship. Each Billing is linked to one Hospital. Each Hospital has many Bills.
Relationship2 (Hospital, Doctor) It is a One-to-Many Relationship. A Hospital has many Doctors. One Doctor is assigned to one Hospital.
Relationship3(Doctor, Patient) It is a Many-to-Many Relationship. A Doctor examines multiple Patients. A Patient meets multiple Doctors.
Relationship4(Hospital, Patient) It is a One-to-Many Relationship. A Hospital admits many Patient. A Patient is admitted to one Hospital at the time of treatment.
Relationship5(Hospital, Medical records) It is a One-to-Many Relationship. A Hospital contains Multiple Medical records. A Medical record is linked to One Hospital.


## Extension (Prerequisite / Billing):
Explain how you modeled billing. In the ER diagram, billing is modeled as an entity to manage financial transactions related to the hospital and patients. This model effectively separates financial data from medical and personal information, maintaining clarity and scalability in the system

## Design Choices:
Brief explanation of why you chose certain entities, relationships, and assumptions
(1) Hospital: Central entity that connects doctors, patients, medical records, and billing. It holds basic information like name, contact, city, and special list.

(2) Doctor: Needed to represent healthcare providers. Attributes include name, ID, specialization, work schedule, and hospital contact.

(3)Patient: Core entity with attributes like full name, DOB, gender, phone number, and address. Patients are central to admissions, meetings with doctors, and billing.

(4)Billing: Modeled as a separate entity to manage financial data independently of patient care data. It allows flexibility for handling payment methods and statuses.

(5)Medical Records: Contains health-related information like diagnoses, treatments, test results, and prescriptions. Tied to both hospital and patient activities.

CHOSEN RELATIONSHIPS:

(1)"Has Assigned" (Hospital–Doctor): One hospital can assign many doctors; a doctor may work in multiple hospitals (M:N relationship).

(2)"Admission" (Hospital–Patient): Patients can be admitted to multiple hospitals over time (M:N), and hospitals can admit many patients.

(3)"Meet" (Doctor–Patient): Represents medical consultations; many doctors can meet many patients (M:N).

(4)"Needs" (Hospital–Medical Records): Indicates that a hospital uses or maintains medical records; a single hospital can maintain many records (1:M).

(5)"Handle" (Hospital–Billing): A hospital handles many billing records; each billing is tied to one hospital (1:M).

ASSUMPTIONS:

1.Each billing record is associated with only one hospital, not directly with a patient, assuming hospitals centrally manage billing.
2.Medical records are maintained per hospital, not directly tied to patients in this model, assuming centralized electronic medical record systems.
3.Doctors may work at more than one hospital, so the relationship with hospitals is many-to-many.
4.Patients can consult multiple doctors, and doctors can see multiple patients, justifying a many-to-many “meet” relationship.
## RESULT
The Entity-Relationship (ER) model was designed to clearly represent the structure and relationships in a hospital management system.
