# Business Education Partnership (BEP)

- Project Lead: Emma Lozhkin 
- Product Manager: Lucy Liu
- Developers:
    - Alan Xie
    - Austin Jiang
    - Sara Fong
    - Gabe Richard 
- Designers:
    - Grace Ma
    - Joslyn Tsui


## Links to relevant documentation

- Statement of Work: https://docs.google.com/document/d/1vmttNBxXfNFZ_KYLp4pNKa4-X3F_RC1V3MR0eF0Xisw/edit?usp=sharing
- Notion BEP Documentation: https://www.notion.so/uwblueprintexecs/4bec9424de924d12b68a2df7a46909b0?v=d39184fe59d54a0f9088fbc4e9377af5

## Summary of Project

Business Entrepreneurship Partnership is a non-profit organization working to connect teachers (educators) with volunteers around the community in order to host workshops, presentations and other events to help educate students on various career oriented topics. BEP’s mission is to help youth have a better understanding of different career paths when it comes time to choose a degree and/or career and better prepare them for the workplace. 

Currently BEP has a functional and active website that serves the basic needs of this organization. However, the website is not very versatile, is visually outdated and could be difficult to navigate for some users. 

Blueprint is working with BEP to build a new and update website application that will serve to match volunteers with educators in a more intuitive manner, and will also allow for easier navigation and changes to code structure in future development of the project. In addition, the backend of the application will be integrated with Salesforce to allow for data management. Salesforce will also serve as a platform for BEP Staff to view all user information. 

## Existing Solutions (either in BP or externally)

Not end-to-end solutions but can we use existing pieces of other projects (e.g. auth)?
Authentication - using OAuth
CRM - using Salesforce. Using this tool came as a request from BEP and Him/Her (their involvement with our project is described more in Notion), but essentially BEP wanted a “non-developer”-friendly tool that they could use to manage the site after we hand the project off to them. We have decided to create an isolated application that communicates with the Salesforce API to display data. 


## Technical Design (write justification for all non-trivial design decisions)

Technology selection (list all alternatives and talk about pros and cons)
Frontend component design - work in progress, will be completed in Spring2020 term
Backend service architecture
 
Tools used:
Salesforce - To compromise with BEP’s request of using Salesforce, we have created an isolated application that communicates with Salesforce’s APIs to pull data from our database and display it on the Salesforce dashboard. 
Pros: makes it easier for BEP to maintain the site after we hand it off to them (non-developer friendly) (tbh not much else)
Cons: tries to abstract away a lot of development so it’s not the most flexible solution. We slightly went around this by creating a separate app instead of using Salesforce’s built in app
 
Contentful (TBD)
OAuth
Heroku

## Scale

-	What scale do we expect? 
expects ~500 visits/month based on current BEP statistics

-	What’s the plan if you need 10x scale?  100x?
    as traffic increases, the number of GPUs increase in Heroku units; may need to pay additional monthly to support more traffic 


## Cost

- What's the estimated cost of running the solution per month or per year?  You'll probably have to make a bunch of assumptions but a ballpark number is good enough. Make sure that the client understands this and is okay with the cost.

Based on Heroku pricing, this will cost around $25/month for production level of traffic, pricing will increase if traffic increases substantially 


## Security/Privacy Considerations

(n/a as of march 2020)

- Are you storing personally identifiable information? 
- Are you using best practices for holding passwords (salting and hashing?)
- Are you sanitizing database input?
