# hospital_db

<h4>Entity Relationship Diagram</h4


 			+---------------------------------------------------------+
                        |			PRESCRIPTIONS			  |
                        +---------------------------------------------------------+
                        | PK prescription_id unsigned int NOT NULL AUTO_INCREMENT |
                        | FK patient_id   (unsigned int)			  |
                        | FK doctor_id    (unsigned int)			  |
                        | medication  VARCHAR(150) NOT NULL			  |
         _ _ _ _ _ _ _ _| prescription_date	DATE NOT NULL 			  |_ _ _ _ _ _ _ _ _ _ _
        |       M       +---------------------------------------------------------+			|
	|												|M
	|												|:		
	|1												|1
	|												|
	|												|
+-----------------------------------------------------+    			 +------------------------------------------------------+
|   PATIENTS    				      |				 |    DOCTORS     					|
+-----------------------------------------------------+    			 +------------------------------------------------------+
| PK personal_id unsigned int NOT NULL AUTO_INCREMENT |				 | PK personal_id unsigned int NOT NULL AUTO_INCREMENT  |
| name VARCHAR(150) NOT NULL			      | 			 | name           VARCHAR(150) NOT NULL			|
| date_of_birth DATE NOT NULL			      |--------------------------| date_of birth  DATE NOT NULL 			|
| address VARCHAR(150) NOT NULL			      |		M:1		 | address	VARCHAR(150) NOT NULL			|
| role	VARCHAR(150) NOT NULL			      |	   			 | role		VARCHAR(150) NOT NULL		        |
| FK doctor_id	(unsigned int)			      |				 | FK hospital_id (unsigned int) 			|
+-----------------------------------------------------+				 +------------------------------------------------------+
                                									 |
                            										M|
                                 									:|
                            										1|
	                         									 |
 				 									 |
							           		+------------------------------------------------------+
								                |			HOSPITALS		       |
								                +------------------------------------------------------+
								                | PK hospital_id unsigned int NOT NULL AUTO_INCREMENT  |
								                | name	VARCHAR(150) NOT NULL			       |
								                | address VARCHAR(150) NOT NULL			       |
								                | size       (unsigned int) 			       |
										| type	VARCHAR(150) NOT NULL			       |
										|accreditation_status VARCHAR(150) NOT NULL	       |
								                +------------------------------------------------------+
