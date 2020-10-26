# The Shoe Project

- Project Lead: Deep Dhillon (@dhillondeep)
- Product Manager: Jenna Hirji
- Developers:
    - Abhijeet Prasad (@AbhiPrasad)
    - Hanlin Cheng (@hanlinc27)
    - Leslie Xin (@lesliexin)
    - Saumya Gupta (@s278gupt)
    - Shehryar Suleman (@Shehryar21)
    - Dinu Wijetunga (@DinuWije)
    - Megan Penny (@m-penny)
- Designers:
    - Joslyn Tsui
    - Amanda Guo

## Links to relevant documentation
- [Statement of Work](https://docs.google.com/document/d/1huV4p6jx7v4qCaa95KBh54_DyLA6bLZ85hl46M74bjc/edit)
- [Notion workspace](https://www.notion.so/uwblueprintexecs/Shoe-Project-ed312d3378594f7fb3b2edd1cf0b0c63)
- [Github Repo](github.com/uwblueprint/shoe-project/)

## Summary of Project
- The Shoe project is an organization dedicated to providing educational opportunities in speaking, writing, 
  leadership to immigrant and refugee women.
- The organization is looking to showcase impact made by stories on their 10th anniversary in 2021.
- Building a web app for the organization to show a canadian map where stories are pins
    - each point on the map will be the city the story originated from
    - filters will added to look for information
    - stories can be previewed and displayed in full page
- This project is scoped to be completed in two terms (F20, W21)
    - The first term will focus on displaying stories, map, and pins
    - The second term will focus on a portal to allow creation, updates, and deletion of stories

## Existing Solutions (either in BP or externally)
- No existing technical solutions found

## Technical Design (write justification for all non-trivial design decisions)
- Technical Stack
    - Go (backend)
        - Fast growing language and provides huge upside learning upside for developers.
        - Backend is not complex and Go has huge array of packages available for project needs.
        - Nice static language with C like syntax so easy to pick up
    - React (frontend)
        - Straightforward to pick up and easy to learn (javascript)
        - Popular library with huge array of package available
    - Postgres
        - Team members have previous experience
        - Popular database with many cool features not available in other RDS
        - Relational database needed to manage entity relationships and queries
    - REST
        - Simple endpoints (GET and POST) and easy to use
- Schema overview
    - Users - authorized (admin) users to add and delete stories
    - Stories - each individual story (text, multimedia)
    - Authors - author for the shoe project stories (basic info, origin location, etc)
- REST endpoints
    - GET /stories - get all stories to display
    - GET /story/{id} - get story by id
    - POST /stories - upload stories in bulk
    - POST /authors - upload authors in bulk
    - POST /login - login using username and password (gives jwt token back)
- Backend architecture
    - Serve react assets using Go
    - REST endpoints
    - Postgres DB (via Gorm)
    - user management - login users and providing jwt token for access
    - positional information - positional information calculations for map pin
    - stories view - endpoints to provide stories information
- Frontend features
    - map view - display canadian map with all stories as pins
    - preview view - preview box when clicked on story pin
    - story view - full story displayed along with multimedia

## Scale
- Web app will be used by the shoe project viewers and educational institutes (exact number unknown)
- Few admin users who can upload stories (only we will upload stories for now)
- Backend is primarily used to server assets and basic REST endpoints so any instance can handle the load
- Go is lightweight and scalable enough to handle huge traffic

## Cost
In conversation with the shoe project team to decide the best pricing!
Looking at a range of $20 to $25 for this project

**Heroku estimate:**
- Hobby dyno - $7
    - Multiple dyno could be added based on load
- Hobby basic Postgres - $9
- Total estimated cost: $16

## Security/Privacy Considerations
- User authentication
    - Using simple username and password stored inside Users table
    - Password is hashed using `bcrypt` password-hashing
    - JWT token valid for few minutes (undecided) is issued
        - This token is needed to make requests to protected endpoints
- No manual inputs are allowed for users so sanitization isn't needed
- Stories don't have any private information and hence no issue with privacy
