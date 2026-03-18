# Work-Order-Analysis-Business-Insights-SQL-Excel-

CREATE DATABASE `work order extract (20)`;

USE `work order extract (20)`;
SHOW tables;
SELECT DATABASE();

CREATE TABLE `GNL WORK ORDER` (
`Order Number` INT PRIMARY KEY,
  `Urgency` VARCHAR(20),
  `Suburb` VARCHAR(20),
  `Claimed Date` DATE,
  `Amount inc` DECIMAL(6,2),
  `Admin` VARCHAR(20)
);


SELECT * FROM `GNL WORK ORDER`;
SHOW tables;
INSERT INTO `GNL WORK ORDER` (`Order Number`, `Urgency`, `Suburb`, `Claimed Date`, `Amount inc`,`Admin` )
VALUES ('1', 'URG', 'papatoetoe', '2026-02-09', 196, 'AIMEE');

INSERT INTO `GNL WORK ORDER`(`Order Number`, `Urgency`, `Suburb`, `Claimed Date`, `Amount inc`,`Admin`)
VALUES ('2', 'URS', 'MANGERE EAST ', '2026-01-15', 456, 'AIMEE');

INSERT INTO `GNL WORK ORDER`(`Order Number`, `Urgency`, `Suburb`, `Claimed Date`, `Amount inc`,`Admin`)
VALUES ('3', 'GNL', 'MANGERE ', '2024-01-15', 632, 'AIMEE');

INSERT INTO `GNL WORK ORDER`(`Order Number`, `Urgency`, `Suburb`, `Claimed Date`, `Amount inc`,`Admin`)
VALUES ('4', 'GNL', 'Otara ', '2025-11-15', 89, 'AMY');

INSERT INTO `GNL WORK ORDER`(`Order Number`, `Urgency`, `Suburb`, `Claimed Date`, `Amount inc`,`Admin`
VALUES ('5', 'GNL', 'Otara ', '2025-11-15', 262, 'AIMEE');

INSERT INTO `GNL WORK ORDER`(`Order Number`, `Urgency`, `Suburb`, `Claimed Date`, `Amount inc`,`Admin`)
VALUES ('6', 'GNL', 'Otara ', '2025-9-15', 22, 'AIMEE');

INSERT INTO `GNL WORK ORDER`(`Order Number`, `Urgency`, `Suburb`, `Claimed Date`, `Amount inc`,`Admin`)
VALUES ('8', 'GNL', 'papatoeote ', '2025-11-15', 695, 'JAMIE');

ALTER TABLE `GNL WORK ORDER` ADD `Admin`VARCHAR(20) DEFAULT'AIMEE';
ALTER TABLE `GNL WORK ORDER` DROP COLUMN `Admin`;

ALTER TABLE `GNL WORK ORDER`
ADD COLUMN `Admin` VARCHAR(20);

SELECT `Order Number`, `Suburb`,`Amount inc` FROM `GNL WORK ORDER`
WHERE `Amount inc`>99
order by `Amount inc`;

SELECT AVG(`Amount inc`), SUM(`Amount inc`), MAX(`Amount inc`),MIN(`Amount inc`)
FROM `GNL WORK ORDER`;

SHOW COLUMNS FROM `GNL WORK ORDER`;
UPDATE `GNL WORK ORDER`
SET `Admin`='JAMIE'
WHERE `Suburb` = 'MANGERE ';

CREATE TABLE `GNL TEAM`(
    `ID` INT AUTO_INCREMENT PRIMARY KEY,
    `NAME` VARCHAR(20) NOT NULL,
    `SEX` VARCHAR(10),
    `SALARY` INT
);

SELECT * FROM `GNL TEAM`;
SHOW tables;

INSERT INTO `GNL TEAM`(`NAME`,`SEX`,`SALARY`) 
VALUES('AIMEE', 'F', 789);

INSERT INTO `GNL TEAM`(`NAME`,`SEX`,`SALARY`) 
VALUES('AMY', 'F', 856);

INSERT INTO `GNL TEAM`(`NAME`,`SEX`,`SALARY`) 
VALUES('JAMIE', 'M', 985);

DROP TABLE `GNL TEAM`;

ALTER TABLE `GNL WORK ORDER`
MODIFY `Admin` VARCHAR(20) NULL;
SET SQL_SAFE_UPDATES = 0;


UPDATE `GNL WORK ORDER`
SET Admin = NULL
WHERE Admin IS NOT NULL 
AND Admin NOT IN (SELECT NAME FROM `GNL TEAM`);

SHOW CREATE TABLE `GNL WORK ORDER`;
SHOW CREATE TABLE `GNL TEAM`;



ALTER TABLE `GNL WORK ORDER`
ADD foreign key (`Admin`)
REFERENCES `GNL TEAM`(`NAME`)
on delete set null;
