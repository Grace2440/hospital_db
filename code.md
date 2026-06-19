<h1>ERD code for DB plan</h1>
Table hospitals { <br>
  hospital_id integer [primary key]<br>
  name varchar<br>
  address varchar<br>
  size integer<br>
  accreditation_status varchar<br>
}<br>

Table doctors {<br>
  personal_id integer [primary key]<br>
  name varchar<br>
  date_of_birth date<br>
  address varchar<br>
  role varchar<br>
  hospital_id integer<br>
}<br>

Table patients {<br>
  personal_id  integer [primary key]<br>
  name varchar<br>
  date_of_birth  date<br>
  address varchar<br>
  role varchar<br>
  doctor_id integer<br>
}<br>

Table prescriptions {<br>
  prescription_id  integer [primary key]<br>
  patient_id  integer<br>
  doctor_id  integer<br>
  medication varchar<br>
  prescription_date  date<br>
}<br>

Ref hospital_id_doctors: hospitals.hospital_id < doctors.hospital_id<br>

Ref: patients.doctor_id > doctors.personal_id<br>
Ref: prescriptions.patient_id > patients.personal_id<br>
Ref: prescriptions.doctor_id > doctors.personal_id<br>

<h1> SQL Query for specified instances</h1>

To print a list of all doctors based at a hospital_id (5):<br>
        SELECT * FROM doctors WHERE hospital_id = 5;<br>
<br>
To print a list of all prescriptions for a patient (105), ordered by the prescription date:<br>
        SELECT * FROM prescriptions WHERE patient_id = 105<br>
        ORDER BY prescription_date ASC;
<p>
To print a list of all prescriptions that doctor (5) has prescribed:<br>
        SELECT * FROM prescriptions WHERE doctor_id = 5;
</p>
<p>
To add a new patient to the database, including being registered with one of the doctors:
        INSERT INTO patients (name, date_of_birth, address, role, doctor_id)<br>
        VALUES ('James Dole', '2000-05-12', '12 Lagos Street', 'Patient', 1);<br></p>
<p>
Identify which doctor has made the most prescriptions:<br>
        SELECT doctor_id, COUNT(*) AS total_prescriptions<br>
        FROM prescriptions<br>
        GROUP BY doctor_id<br>
        ORDER BY total_prescriptions DESC<br>
        LIMIT 1;<br></p>
<p>
Print a list of all doctors at the hospital with biggest size(number of beds):<br>
        SELECT d.personal_id, d.name, h.name AS hospital_name, h.size<br>
        FROM doctors d<br>
        JOIN hospitals h ON d.hospital_id = h.hospital_id<br>
        WHERE h.size = (<br>
                SELECT MAX(size)<br>
                FROM hospitals<br>
                        );<br>
</p>
