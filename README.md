# Healthcare OLTP to Data Warehouse Project

## 📚 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Dataset Sources](#dataset-sources)
- [High-level DW & BI Solution Architecture](#high-level-dw--bi-solution-architecture)
- [Description of the data warehouse dimensional model](#description-of-the-data-warehouse-dimensional-model)

## Overview

This project involves designing and implementing a Data Warehousing and Business Intelligence (DW & BI) solution using a healthcare-related OLTP dataset. The goal is to enable effective analytics and reporting by transforming transactional healthcare data into a dimensional star schema format using ETL processes.

## Dataset
https://synthea.mitre.org/downloads

The dataset used is a patient medical dataset. The dataset consists of 18 entities. They are as follows,
1.	Allergies
2.	Patients
3.	Claims
4.	Claims transactions 
5.	Care plans
6.	Conditions
7.	Devices
8.	Encounters
9.	Imaging studies 	10.	Immunizations
11.	Medications
12.	Observations
13.	Organizations
14.	Payer transitions
15.	Payers
16.	Procedures
17.	Providers
18.	Supplies

![ER Diagram](https://drive.google.com/uc?export=view&id=1WohbTvUpQ5sgv4fczP7dBMf1sdwMdI_6)

## Dataset Sources
- .csv: All tables except Allergies
- .txt: Allergies

## High-level DW & BI Solution Architecture

![High-level DW & BI solution architecture](https://drive.google.com/uc?export=view&id=1scnqqerQ3plLR1PPxo6Ij0tUCGdJFi3W)

## Description of the data warehouse dimensional model

This is a Star schema dimensional model containing one fact table and five dimension tables.
Patients, Providers, Payers and Organizations are slowly changing dimensions.
**Dim Providers** - Details healthcare professionals
**Dim Organizations** - Stores information about healthcare organizations
**Dim Patients** - Includes all patients’ details
**Dim Payers** - Contains information about insurance providers, including coverage statistics and revenue
**Dim Date** – Instead using the date we store a key to a particular date.

Assumptions Made for the Design
- Assume Encounter table as the fact table because it contains more foreign keys and stores metrics and measures related to healthcare encounters, such as base encounter cost, total claim cost, and payer coverage. 
- Assume providers, patients, organizations, and payers as dimension tables because the encounter table contains their foreign key.
-Assume Patients, Providers, Payers and Organizations are slowly changing dimensions because they may change over time


