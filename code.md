<h1>ERD code for DB plan</h1>
Table hospitals {
  hospital_id integer [primary key]
  name varchar
  address varchar
  size integer
  accreditation_status varchar
}

Table doctors {
  personal_id  integer [primary key]
  name varchar
  date_of_birth  date
  address varchar
  role varchar
  hospital_id integer
}

Table patients {
  personal_id  integer [primary key]
  name varchar
  date_of_birth  date
  address varchar
  role varchar
  doctor_id integer
}

Table prescriptions {
  prescription_id  integer [primary key]
  patient_id  integer
  doctor_id  integer
  medication varchar
  prescription_date  date
}

Ref hospital_id_doctors: hospitals.hospital_id < doctors.hospital_id // many-to-one

Ref: patients.doctor_id > doctors.personal_id
Ref: prescriptions.patient_id > patients.personal_id
Ref: prescriptions.doctor_id > doctors.personal_id

<h1> SQL Query for specified instances</h1>

To print a list of all doctors based at a hospital_id (5):
        SELECT * FROM doctors WHERE hospital_id = 5;
To print a list of all prescriptions for a patient (105), ordered by the prescription date:
        SELECT * FROM prescriptions WHERE patient_id = 105
        ORDER BY prescription_date ASC;
To print a list of all prescriptions that doctor (5) has prescribed:
        SELECT * FROM prescriptions WHERE doctor_id = 5;
To add a new patient to the database, including being registered with one of the doctors:
        INSERT INTO patients (name, date_of_birth, address, role, doctor_id)
        VALUES ('James Dole', '2000-05-12', '12 Lagos Street', 'Patient', 1);
Identify which doctor has made the most prescriptions:
        SELECT doctor_id, COUNT(*) AS total_prescriptions
        FROM prescriptions
        GROUP BY doctor_id
        ORDER BY total_prescriptions DESC
        LIMIT 1;
Print a list of all doctors at the hospital with biggest size(number of beds):
        SELECT d.personal_id, d.name, h.name AS hospital_name, h.size
        FROM doctors d
        JOIN hospitals h ON d.hospital_id = h.hospital_id
        WHERE h.size = (
                SELECT MAX(size)
                FROM hospitals
                        );

