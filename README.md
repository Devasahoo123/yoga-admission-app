ER Diagram for Yoga Admission Form
The Yoga Admission Form involves two main entities: Participant and Payment. Below is the representation of these entities and their relationships.

Entities:
Participant
Attributes:
id (Primary Key, Auto Increment)
name (String)
age (Integer)
email (String)
phone (String)
batch (Enum: '6-7AM', '7-8AM', '8-9AM', '5-6PM')
payment_status (Boolean)
Payment
Attributes:
payment_id (Primary Key, Auto Increment)
participant_id (Foreign Key referencing Participant.id)
payment_date (Date)
amount (Decimal)
status (Enum: 'Paid', 'Failed', 'Pending')
Relationships:
A Participant can have multiple Payments (One-to-Many). This allows a participant to make payments every month.
Each Payment is associated with a single Participant using participant_id (Foreign Key).
ER Diagram Representation:
lua
Copy
Edit
  +------------------+             +------------------+
  |   Participant    |             |      Payment     |
  +------------------+             +------------------+
  | id (PK)          |<--------+    | payment_id (PK)  |
  | name             |         |    | participant_id (FK) |
  | age              |         |    | payment_date      |
  | email            |         |    | amount            |
  | phone            |         |    | status            |
  | batch            |         |    +------------------+
  | payment_status   |         |
  +------------------+         |
                               |
                               |
                               |
                    +--------------------------+
                    |    Payment Relationship   |
                    +--------------------------+
Database Schema
Here’s the SQL script to create the tables:

sql
Copy
Edit
CREATE TABLE Participant (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    age INT NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(10) NOT NULL,
    batch ENUM('6-7AM', '7-8AM', '8-9AM', '5-6PM') NOT NULL,
    payment_status BOOLEAN DEFAULT FALSE
);

CREATE TABLE Payment (
    payment_id INT AUTO_INCREMENT PRIMARY KEY,
    participant_id INT,
    payment_date DATE NOT NULL,
    amount DECIMAL(10, 2) DEFAULT 500,
    status ENUM('Paid', 'Failed', 'Pending') DEFAULT 'Pending',
    FOREIGN KEY (participant_id) REFERENCES Participant(id)
);
Sample Data
Below is a sample set of data that would be stored in the Participant and Payment tables:

Participant Table
id	name	age	email	phone	batch	payment_status
1	Devanand Sahoo	23	devasahow085@gmail.com	8090601096	8-9AM	Paid
2	Devanand Sahoo	22	devasahoo1@gmail.com	8090601096	7-8AM	Paid
3	Kartik	21	devasah2385@gmail.com	8090601096	8-9AM	Paid
4	Test	22	test@gmail.com	1234567890	7-8AM	Paid
5	Test2	44	test23@gmail.com	0987654321	8-9AM	Paid
6	dd Sahoo	22	devasahoo0852@gmail.com	8090601096	8-9AM	Paid
15	22 Sahoo	22	devasa5@gmail.com	0800601096	8-9AM	Paid
Payment Table
payment_id	participant_id	payment_date	amount	status
1	1	2025-06-01	500	Paid
2	2	2025-03-01	500	Paid
3	3	2025-07-01	500	Paid
4	4	2025-06-01	500	Paid
5	5	2025-07-01	500	Paid
6	6	2025-11-01	500	Paid
7	15	2025-12-01	500	Paid
This structured format in the README will make it very clear for anyone reading it to understand the database schema, relationships, and how the data is stored.
