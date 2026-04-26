# Database-Modelling
# Student: Askhatov Amir
# Course: CP2404 – Database Modelling

📋 Project Overview
This repository contains the database design and implementation for an Airline Charter Management System. The system models the full lifecycle of a charter airline operation — from employee and crew management to aircraft maintenance, bookings, billing, and customer membership.

🗂️ Database Schema
The EER diagram covers the following entities and relationships:


👤 Employee & Staff
EntityDescriptionEMPLOYEECore staff table with self-referencing supervisor FKADMIN_STAFFSpecialisation of EMPLOYEE; handles billing and resourcesCREWSpecialisation of EMPLOYEE; further split into PILOT and CABIN_ATTENDANTPILOTStores pilot licence and test datesCABIN_ATTENDANTStores physical/language attributesDIVISIONOrganisational unit; each has one managerSALARY_HISTORYTracks all salary changes; current = record with no end_date

Specialisation constraint: EMPLOYEE is totally and disjointly specialised into CREW and ADMIN_STAFF. CREW is further totally and disjointly specialised into PILOT and CABIN_ATTENDANT.


✈️ Aircraft & Flights
EntityDescriptionAIRCRAFT_TYPEAircraft models (e.g. Cessna, Embraer) with capacity and weight specsAIRCRAFTIndividual aircraft with engine number, purchase info, and warrantyFLIGHTFlight records linking aircraft to departure/arrival detailsAIRCRAFT_REPAIRRepair logs including fault codes, costs, and technician comments


🏨 Resources
EntityDescriptionRESOURCESuperclass for physical resourcesACCESS_CARDCard with pin, unlock code, and access locationLOCKERLocker with floor numberRESOURCE_ASSIGNMENTTracks assignment and return of resources to admin staff


💳 Customers & Bookings
EntityDescriptionCUSTOMERCustomer details with membership and contact infoMEMBERSHIP_CATEGORYDiscount tiers applied at billing timeBOOKINGLinks a customer to a booking date and statusBOOKING_FLIGHTJunction table: which flights are in each booking, with seat/class info


💰 Billing & Payments
EntityDescriptionBILLGenerated per completed flight by admin staffPAYMENTSupports multiple partial payments with different payment modes


🎓 Training
EntityDescriptionTRAININGTraining programmes with cost and scheduleCREW_TRAININGTracks crew attendance, score, and grade per training session

The 20-training limit per crew member is enforced at the application level.


📐 Design Assumptions

Aircraft types store model-level info; individual AIRCRAFT records store instance-level details (engine number, purchase date, warranty).
Every employee has exactly one supervisor (self-referencing FK) and belongs to one DIVISION.
The current salary is the SALARY_HISTORY record where end_date is NULL.
Customer discounts are derived from MEMBERSHIP_CATEGORY at the time of billing.
A BILL is generated per completed flight by an admin staff member.


⚠️ Limitations

Cargo-only trips are not modelled; design focuses on passenger charter trips.
Access card locations are stored as VARCHAR; a separate LOCATION entity could support granular access control.
Aircraft repair does not track parts inventory — only faulty part descriptions are recorded.


🛢️ SQL Practical

🚧 Coming Soon

SQL scripts for schema creation, sample data insertion, and queries will be added here shortly. This will include:

CREATE TABLE statements with all constraints and foreign keys
Sample INSERT data for testing
Query examples covering joins, aggregations, and subqueries


🛠️ Tools Used

MySQL Workbench – EER diagram design (.mwb)
MySQL – Target DBMS for SQL implementation


📄 License
This project is submitted as academic coursework for CP2404 at James Cook University. Not for redistribution.ShareContentpdfAssignment1_AskhatovAmir.mwbmwbpdf
