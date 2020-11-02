# Architecture Design Documentation

# Project Name: Building Up

**Contributors:** 

- Faizaan Madhani (PL)
- Angelina Jin (PM)
- Developers:
    - Alex Guo
    - Allyn Zheng
    - Anand Issac
    - Michael Meng
    - Raveen Singh
    - Samantha Orizabal
    - Tony Zhao
- Designers:
    - Grace Ma
    - Shaahana Naufal

## **Links to relevant documentation**

[Project Details](https://www.notion.so/Project-Details-6780acf25c614e13b06dc1cff1ae22f5) 

[Client Clarification and Feature Priority](https://www.notion.so/Client-Clarification-and-Feature-Priority-751af3d787e84162b3ddf0ac4d7ae7b9) 

## **Summary of Project**

We are building an online platform to enable Building Up to fundraise for their Toque Campaign. 

That is, we are building a system that allows teams and individuals at a school to sign up and start fundraising by selling toques. Each user of a team receives a link to storefront they can share with potential donors to buy toques. When a user buys a toque, the record is stored in relation to the team that they bought it from and the system keeps track of how much the team has fundraised and sold and how they compare to other teams and schools (in the form of a leaderboard). Each team has their own page which can be publicly seen to show their fundraising numbers. 

The client is able to manage their inventory, view payments and manage products specification on the Shopify Overview Dashboard. Finally, they're able to manage and get a complete view of all the teams and general fundraising on the admin dashboard. 

## **Existing Solutions (either in BP or externally)**

**Inspiration (Technical and Non-Technical)**

- E-Commerce apps are plenty. Raising the roof has even hired a third party web-design agency known as White Board Creative to build them a storefront for their main website. Though Blueprint is unable to directly plug into what they are building (as it is a Wordpress site), we are using their designs the inform how we design our app to ensure that there are enough similarities.
- Within Blueprint, the general architecture that Paramedics took to building out their platform (Node.JS + GraphQL + Postgres + Sequelize ORM backend, and a React Frontend) became the initial inspiration for the technical design for Building Up.

**Third Party Tools and Frameworks**

- Shopify
    - Used to process payments, allows the clients to manage inventory and product and prevents Blueprint from building out an entire CMS and inventory management system for RTR.
- Apollo GraphQL
    - Our frontend and backend is building on top of Apollo, specifically apollo-express-server in the backend. It powers GraphQL querying.

**Libraries and Dependancies:**

- BCryptJS
    - Hashing, Salting and Authentication — ensure we don't store passwords in plain text
- Material UI
    - Reusable, nice-looking components that we wrap and stylize

## **Technical Design (write justification for all non-trivial design decisions)**

**Frontend:**

- React
    - Commonly used across Blueprint
    - Reusable components
    - **React Router** can be used for store pages, team pages, etc.
- Redux
    - Persistent State Container that works across the application
    - Used to store state that is accessible to components anywhere in the app which is useful for things like persisting login.

**Backend:**

- NodeJS (Apollo GraphQL, Express)
    - NodeJS is a very common language for server-side web development
    - Why GraphQL?
        - GraphQL makes it easy to query our backend and retrieve information instead of fetching through multiple endpoints. We can decide on a singular GraphQL schema design which is then easy to understand and connect to the code that developers write.
        - It proves a simple framework to understanding the API that we write and makes it easy for developers to see what's going on.
        - **Subscriptions** are also a key reason. We can have our frontend subscribe to useful fields in the database for teams, such as the amount of money they've raised and render that on the frontend in near real-time without having to worry too much about websockets.

**Database:**

- **Postgres**
    - We need relational data as the client needs to store teams in relation to schools and purchases need to be related to teams
    - Additionally, the client wants data to be easily exported into spreadsheets. Postgres allows easy exporting to csv.
- **Redis**
    - The Redis Cache will be used to keep track of a leaderboard of the team fundraising/toque sales numbers
    - Redis is very fast, and we're using ZSETs (Sorted Sets) to keep a running ordered list of the teams that will be periodically fetched to update the score.
        - We've built our own simple DAO to manage leaderboards in Redis, and to allow other parts of the application to manipulate the Redis leaderboard with ease
- **Sequelize**
    - An ORM to make interacting with Postgres easier for simple database querying.

For diagrams (eg. of the user flows), refer here:

[Diagrams](https://www.notion.so/Diagrams-1a0f8003249d4fd294dbce5ea8aa91ef)

For a full breakdown of what we're trying to build between the two semesters this project is scoped for, refer here:

[What we're building](https://www.notion.so/What-we-re-building-dbf2ea057a1f4ea0bda19de0a952e8b1)

For a breakdown of our GraphQL and Database Schemas, and Redis Data Structures, which help inform how our API is built, refer here:

[Schemas and Data Structures](https://www.notion.so/Schemas-and-Data-Structures-dee408a78b7b4f5a9d50cb18f0ada174)

## **Scale**

RTR is unsure about this, but could include a couple thousand users

## **Cost**

Summary of Costs are as follows:

**Heroku + Google Cloud Storage + Shopify Basic (Frontend, Backend, Database, Redis, Cloud Storage)**

Starts at $0 Hosting, DB and Redis + $0.20 Cloud Storage + $29.99 Shopify Basic =**$30.19/month**

For a full breakdown of the costs and for a detailed understanding of the options presented to the client (client chose Option 1), refer to the page below:

[DB and Hosting Costs](https://www.notion.so/DB-and-Hosting-Costs-f5458858539d4a7daf034f5b5557df33)

## **Security/Privacy Considerations**

What are we storing?

- User names, emails, passwords, purchases

How are we maintaining data integrity?

- User names and emails are kept in a db in plain text form
- Passwords are salted and hashed using BCRYPT and stored as hashes.
- Purchases, being processed through Shopify, are stored there. We store purchase records in the database and maintain a running total of the fundraised total and toques sold in the database, which are updated via webhooks from Shopify.

Since processing payments can be tricky to keep secure, and we are relying on Shopify's pre-built checkout for security.