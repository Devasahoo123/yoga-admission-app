ER Diagram for the Yoga Admission Form that will be used to store the data in the database. I’ll break down the entities and relationships for you:

Entities
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
Relationships
Participant has Payment (One-to-One or One-to-Many, depending on payment model. For simplicity, it’s One-to-Many, since a participant can pay every month.)
A participant can make multiple payments (one for each month), so we associate the participant_id in the Payment table.
ER Diagram Representation
Here’s a simple textual representation of the ER diagram:

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
Explanation of Fields
Participant Table:

id: Unique identifier for each participant.
name: Name of the participant.
age: Age of the participant (used for validation, between 18-65).
email: Email of the participant.
phone: Phone number for communication (must be validated as 10 digits).
batch: The batch they’ve enrolled in (one of the four time slots).
payment_status: Indicates whether the participant has completed the payment for the month.
Payment Table:

payment_id: Unique identifier for each payment.
participant_id: Foreign Key referencing the Participant.id, establishing a relationship with the participant.
payment_date: The date on which the payment was made.
amount: The amount paid (always 500).
status: Indicates whether the payment was successful (Paid), failed (Failed), or is pending.
Database Schema
Here’s the SQL script for creating the tables:

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
Entity Relationship Summary
A Participant can enroll in a batch and make multiple payments over time (every month).
Each Payment is linked to a specific Participant.


Stored data:
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|  id  |       name        |  age  |           email            |     phone      |   batch   |  payment_date    | payment_status     |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|   1  | Devanand Sahoo    |   23  | devasahow085@gmail.com      | 8090601096     |  8-9AM    | 2025-06          | Paid               |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|   2  | Devanand Sahoo    |   22  | devasahoo1@gmail.com        | 8090601096     |  7-8AM    | 2025-03          | Paid               |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|   3  | Kartik            |   21  | devasah2385@gmail.com       | 8090601096     |  8-9AM    | 2025-07          | Paid               |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|   4  | Test              |   22  | test@gmail.com              | 1234567890     |  7-8AM    | 2025-06          | Paid               |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|   5  | Test2             |   44  | test23@gmail.com            | 0987654321     |  8-9AM    | 2025-07          | Paid               |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|   6  | dd Sahoo          |   22  | devasahoo0852@gmail.com     | 8090601096     |  8-9AM    | 2025-11          | Paid               |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+
|  15  | 22 Sahoo          |   22  | devasa5@gmail.com           | 0800601096     |  8-9AM    | 2025-12          | Paid               |
+------+-------------------+-------+----------------------------+----------------+-----------+------------------+--------------------+

							
