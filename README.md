# Clinic
Database
CREATE DATABASE Veterinary;
USE Veterinary;

CREATE TABLE doctor (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    specialization VARCHAR(100) NOT NULL
);


CREATE TABLE patients (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    species VARCHAR(50) NOT NULL,
    breed VARCHAR(50),
    date_of_birth DATE,
    owner_name VARCHAR(100) NOT NULL,
    owner_contact VARCHAR(20),
    medical_history TEXT,
    allergies TEXT,
    vaccinations TEXT
);


CREATE TABLE appointments (
    id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT,
    appointment_date DATETIME,
    duration_minutes INT,
    remarks TEXT,
    FOREIGN KEY (patient_id) REFERENCES patients(id),
    FOREIGN KEY (doctor_id) REFERENCES doctor(id)
);


CREATE TABLE inventory_items (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    quantity INT,
    reorder_point INT
);



CREATE TABLE invoices (
    id INT PRIMARY KEY,
    appointment_id INT,
    amount DECIMAL(10, 2),
    paid BOOLEAN DEFAULT NULL,
    payment_date DATE,
    inventory_item_id INT,
    FOREIGN KEY (appointment_id) REFERENCES appointments(id),
    FOREIGN KEY (inventory_item_id) REFERENCES inventory_items(id)
  );


CREATE TABLE financial_records (
    id INT PRIMARY KEY,
    invoice_id INT,
    transaction_date DATE,
    description TEXT,
    amount DECIMAL(10, 2),
    FOREIGN KEY (invoice_id) REFERENCES invoices(id)
);



INSERT INTO doctor (id, name, specialization) VALUES
(1, 'Dr. Smith', 'Internal Medicine'),
(2, 'Dr. Johnson', 'Surgery'),
(3, 'Dr. Lee', 'Dermatology'),
(4, 'Dr. Anderson', 'Radiology');


INSERT INTO patients (id, name, species, breed, date_of_birth, owner_name, owner_contact, medical_history, allergies, vaccinations) VALUES
(1, 'Fluffy', 'Cat', 'Persian', '2019-05-15', 'John Doe', '555-1234', 'No major medical issues', 'None', 'Rabies, FVRCP'),
(2, 'Buddy', 'Dog', 'Golden Retriever', '2018-10-10', 'Jane Smith', '555-5678', 'Hip dysplasia', 'Peanuts', 'Rabies, DHPP'),
(3, 'Max', 'Dog', 'Labrador Retriever', '2017-08-20', 'Sarah Johnson', '555-9876', 'No major medical issues', 'None', 'Rabies, DHPP'),
(4, 'Whiskers', 'Cat', 'Siamese', '2020-02-12', 'Michael Davis', '555-4321', 'Asthma', 'Fish', 'Rabies, FVRCP');



INSERT INTO inventory_items (id, name, description, quantity, reorder_point) VALUES
(1, 'Medicine A', 'For pain relief', 50, 10),
(2, 'Medicine B', 'Antibiotic', 30, 5),
(3, 'Medicine C', 'Antifungal', 20, 5),
(4, 'Medicine D', 'Anti-inflammatory', 15, 3);


INSERT INTO appointments (id, patient_id, doctor_id, appointment_date, duration_minutes, remarks) VALUES
(1, 1, 1, '2023-07-15 10:00:00', 30, 'Routine check-up'),
(2, 2, 2, '2023-07-16 14:30:00', 60, 'Annual vaccination'),
(3, 3, 3, '2023-07-17 11:30:00', 45, 'Skin check-up'),
(4, 4, 4, '2023-07-18 09:00:00', 30, 'Annual vaccination');


INSERT INTO invoices (id, appointment_id, amount, paid, payment_date) VALUES
(1, 1, 50.00, true, '2023-07-15'),
(2, 2, 100.00, false, null),
(3, 3, 80.00, false, null),
(4, 4, 60.00, true, '2023-07-18');


INSERT INTO financial_records (id, invoice_id, transaction_date, description, amount) VALUES
(1, 1, '2023-07-15', 'Payment received', 50.00),
(2, 2, '2023-07-15', 'Payment received', 100.00),
(3, 3, '2023-07-17', 'Invoice generated', 80.00);
