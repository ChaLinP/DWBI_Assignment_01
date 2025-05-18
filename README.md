# Healthcare OLTP to Data Warehouse Project

## 📚 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Dataset Sources](#dataset-sources)
- [High-level DW & BI Solution Architecture](#high-level-dw--bi-solution-architecture)

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

![ER Diagram](https://drive.google.com/file/d/1WohbTvUpQ5sgv4fczP7dBMf1sdwMdI_6)

## Dataset Sources
- .csv: All tables except Allergies
- .txt: Allergies

## High-level DW & BI Solution Architecture

![High-level DW & BI solution architecture](https://drive.google.com/uc?export=view&id=1scnqqerQ3plLR1PPxo6Ij0tUCGdJFi3W)


