# Region of Waterloo Paramedic Services (ROWPS)

- Project Lead: Peter Song (@petorsong)
- Developers:
	- Aaron Abraham (@aaronabraham311)
	- Carelynn Tsai (@carelynntsai)
	- Daniel Chen (@danielchen115)
	- Jason Guo (@JasonYG)
	- Jeffrey Kam (@lazypanda10117)
	- Ricky Mao (@rickrm)
- Product Manager: Rishabh Patni
- Designers:
	- Charmaine Wang
	- Gracie Xia
	- Joe Li

## Links to relevant documentation

-	[Statement of work](https://docs.google.com/document/d/11omQuizb0RjQG6-ynfOJr6mn_birUFtSVUMyLnqUAkY/edit?usp=sharing)
- [Initial technical scoping](https://www.notion.so/uwblueprintexecs/2019-Technical-Doc-6e1dfdf27536441cbce8234819384ba6)
- [Notion workspace](https://www.notion.so/uwblueprintexecs/Region-of-Waterloo-Paramedic-Services-396794328ff14336a1c759e84e83b370)

## Summary of Project

- ROWPS is looking for a solution to coordinate personnel and keep track of patients during events with an unusually high number of patients (e.g. Homecoming, St. Patrick's Day @ Ezra Ave.)
- We will build and deliver an iPad application to be used by paramedics on the scene to manage patients and a web application to be used for monitoring
- This project is scoped to be completed in two terms (W20, S20)
  - The first term will focus on developing the backend and beginning on the web frontend
  - The second term will focus on completing the web and mobile clients

## Existing Solutions (either in BP or externally)

-	No existing technical solutions found

## Technical Design

-	Technology stack
    * React
        * over other options: straightforward to pick up, lots of resources available online
    * GraphQL
        * over REST endpoints: fits better with dual web + mobile usage, less backend overhead
    * Node
        * over other options: works well with GraphQL, lots of resources available online
    * Postgres
        * over other relational databases (e.g. MySQL): team members had previous experience
        * over non-relational databases (e.g. Firebase, MongoDB): entity relationships were important enough to go with a relational DB
    * React Native _(not set in stone)_
        * over Swift/Objective C: React components may be transferrable, doesn't require developing on a Mac
- Schema overview
  - Note: database schema and GraphQL API have the exact same structure due to the GraphQL architecture
  - Users - authorized users of the application; primarily paramedic supervisors and commanders
  - Events/Incidents - an overarching event (e.g. St. Patricks Day) will have child incidents (e.g. Ezra Ave)
  - Resources - static lists of ambulances/hospitals
  - Patients - patient information (e.g. triage levels, current status, age, gender, etc.)
-	Frontend features - to be determined/designed, but will include the following:
    - account management - login, authentication, authorization, creating new accounts
    - event management - creating and modifying events
    - dashboard view - overall view of patients, triage levels, statuses, etc.
    - patient management - creating and modifying patient entries
    - resource management - assigning ambulances & hospitals to events
-	Backend service architecture
    - Frontend clients (web/mobile)
    - GraphQL + Node server
    - Postgres DB (via Sequelize ORM)
- Proposed Deployment Details
  - Automated deployment through AWS and Docker
  - AWS services: 1 EC2 instance + 1 RDS instance
    * EC2 instance will host the frontend and backend servers
    * RDS instance will host the database - RDS chosen for reliable backups and recovery guarantees

## Scale

-	iPad app will be deployed to 3-5 devices to be used on site
- Only paramedic supervisors will have access - up to 20 users
- Web application/dashboard may have more users (up to 20 more) but will be mostly read-only
-	Node backend will be built scalable from the ground up, also relatively easy to spin up more AWS EC2 containers if necessary
  - App will only see use a few times throughout the year; overall uptime (or active use) looks to be low
  - Even so, we will have the service up and running throughout - easier for deployment

## Cost

- previously quoted ~$50/month each for 2 environments (test + prod)
- assuming 1 EC2 instance and 1 RDS instance
  - EC2: 720 (hours) * 0.018 ($/hour) = $12.96/month
  - RDS: 720 (hours) * 0.0255 ($/hour) = $18.36/month
 - total: $31.32/month (per environment)

## Security/Privacy Considerations

- Due to the PHIPA regulation, we will not be storing any personally identifiable information in our databases
- Not sure exactly how authentication will work yet - will try to leverage existing LDAP authentication they seem to be using
  - Otherwise we will be handling account management within our solution (users, passwords, permissions, etc.)
- Not many fields with freeform input but they will be sanitized
- Overall there will not be many users with access and every user will have different authorization levels for specific features
