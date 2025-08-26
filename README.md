DROP TABLE IF EXISTS FeePayments;

CREATE TABLE FeePayments (
    payment_id   INT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    amount       DECIMAL(10,2) CHECK (amount > 0),
    payment_date DATE
);

START TRANSACTION;

INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (1, 'Ashish', 5000.00, '2024-06-01');

INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (2, 'Smaran', 4500.00, '2024-06-02');

INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (3, 'Vaibhav', 5500.00, '2024-06-03');

COMMIT;

SELECT * FROM FeePayments;

START TRANSACTION;

INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (4, 'Kiran', 4000.00, '2024-06-04');

INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (1, 'Ashish', -2000.00, '2024-06-05');

ROLLBACK;

SELECT * FROM FeePayments;

CREATE PROCEDURE demo_part_b()
BEGIN
  DECLARE EXIT HANDLER FOR SQLEXCEPTION
  BEGIN

    ROLLBACK;
  END;

  START TRANSACTION;
  INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
  VALUES (4, 'Kiran', 4000.00, '2024-06-04');

  INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
  VALUES (1, 'Ashish', -2000.00, '2024-06-05');

  COMMIT;
DELIMITER ;

CALL demo_part_b();

SELECT * FROM FeePayments;

START TRANSACTION;

INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (5, 'Rahul', 4700.00, '2024-06-06');

INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (6, NULL, 3000.00, '2024-06-07');

ROLLBACK;

SELECT * FROM FeePayments;

CREATE PROCEDURE demo_part_c()
BEGIN
  DECLARE EXIT HANDLER FOR SQLEXCEPTION
  BEGIN
    ROLLBACK;
  END;

  START TRANSACTION;
  INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
  VALUES (5, 'Rahul', 4700.00, '2024-06-06');

  INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
  VALUES (6, NULL, 3000.00, '2024-06-07');

  COMMIT;
DELIMITER ;

CALL demo_part_c();

SELECT * FROM FeePayments;

START TRANSACTION;
INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (7, 'Meena', 5200.00, '2024-06-08');
COMMIT;

SELECT * FROM FeePayments;

START TRANSACTION;
INSERT INTO FeePayments (payment_id, student_name, amount, payment_date)
VALUES (8, 'Zara', 5100.00, '2024-06-09');
COMMIT;

SELECT COUNT(*) FROM FeePayments WHERE payment_id = 8; 
COMMIT;

START TRANSACTION;
SELECT COUNT(*) FROM FeePayments WHERE payment_id = 8;  
COMMIT;
