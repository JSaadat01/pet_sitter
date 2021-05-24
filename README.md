# Pet Sitter App Project

This is hte Readme.md file for my week-6 fundamental project for QA.

## Contents :
* [Brief](#brief)
   * [Additional Requirements](#additional-requirements)
   * [My Approach](#my-approach)
* [Architecture](#architecture)
   * [Database Structure](#database-structure)
   * [CI Pipeline](#ci-pipeline)
* [Project Tracking](#project-tracking)
* [Risk Assessment](#risk-assessment)
* [Testing](#testing)
* [Front-End Design](#front-end-design)
* [Known Issues](#known-issues)
* [Future Improvements](#future-improvements)
* [Authors](#authors)

## Brief / Specification
I have been asked to produce a CRUD application which allows me utilize 'Create', 'Read', 'Update' and 'Delete' functions within an integrated relational database. In order to successfully fulfil this criteria, I have utilised supporting tools, methodologies and technologies that have been shown throughout the core modules covered during training.

The purpose of this project is to emonstrate that I have learnt technical skills over the course of my first few weeks at QA.

### Additional Requirements
In order to successfully meet the specifications of this project, I have included the following supporting tools in my project.

* A Trello board.
* A relational database, which models a clear relationship.
* Clear documentation of the design phase, app architecture and risk assessment.
* A python-based functional application that follows best practices and design principles.
* Test suites for the application, which will include automated tests for validation of the application.
* A front-end website, created using Flask.
* Code integrated into a Version Control System which will be built through a CI server and deployed to a cloud-based virtual machine i.e. Git, Jenkins and GCP.

### Methodology
To achieve the required specification, I have created a simple Pet Sitter app which is a front-end web application that illustrates the  relation between users and their pets. It will allow a user to input 1 or more users and attribute one or more pets to the user(s).

* Create Owner/Pet fields which (satisfies 'Create') that stores:
   * *First Name*
   * *Last Name*
   * *Age*
   * *Address*
   * *Postcode*
   * *Pet's Name*
   * *Pet's Age*
   * *Pet's Colour*
   * *Pet's Species*
   * *Pet's Breed*
   * *Pet's Registered Address*
   * *Pet's Registered Postcode*
* View the user created owner and pet fields (satisfies 'Read')
* Update the existing user created owner and pet fields (satisfies 'Update')
* Delete an existing user created owner or pet field (satisfies 'Delete')

## Architecture
### Database Structure
Pictured below is an entity relationship diagram (ERD) showing the structure of the database.

![ERD](https://imgur.com/a/8sHbNev)

As shown in the ERD, the app models a one-to-many relationship between owner and pet entities using an association table. This allows a user to create an owner entity and associate more than one pet with each owner.

### CI Pipeline
![ci][ci]

 Above is the continuous integration pipeline with the associated frameworks and services related to them. This purpose of the pupline is to ensure the successive and automated development-to-deployment via automation of the integration processes. I can produce code on my local machine and push it to GitHub. The automation tools in place will then allow for new code to be pushed to Jenkins via a webhook to be automatically installed on the google cloud's Virtual Machine. At this point, the tests are then automatically executed and reports which illustrate the results are produced. In addition to this, A seperate testing environment for the app is  run within debugger mode which will allow for successive dynamic testing.

This process is handled by a Jenkins 'pipeline' job with incremental build stages. The perfect design of Jenkins is such that it will output detailed information for a failed job. For example, if a previous build stage fails, the job will fail altogether and provide you with detailed information as to where this occurred. The more modular you make the system is made, the easier it is to pinpoint where the code is failing. This is because more incremental stages makes distinguishing easier. As pictured below, the four build stages are:
* 'Checkout SCM' (pull code from Git respository)
* 'Build' (would be more accurately named 'Installation' as Python doesn't require building, in the strictest sense)
* 'Test' (run pytest, produce coverage report) 
* 'Run' (start the flask-app service on the local VM, belonging to systemctl)

![buildstages][buildstages]

Once the app is considered stable, it is then pushed to a separate VM for deployment. This service is run using the Python-based HTTP web server Gunicorn, which is designed around the concept of 'workers' who split the CPU resources of the VM equally. When users connect to the server, a worker is assigned to that connection with their dedicated resources, allowing the server to run faster for each user.

## Project Tracking
Trello was used to track the progress of the project (pictured below). You can find the link to this board here: https://trello.com/b/ateuNpyv/planning-your-day-a-kanban-template

![trello][https://trello.com/b/ateuNpyv/planning-your-day-a-kanban-template]

The board has been designed such that elements of the project move from left to right from their point of conception to being finished and fully implemented. Each card is also colour-coded according to which element of the project it pertains. From left to right, these lists are:
* *Project Requirements*
   A list of requirements set out in the brief in order for this to be a successful project.
* *Project Resources*
   List of relevant resources for quick access.
* *User Stories*
   Any functionality that is implemented into the project first begins as a user story. This keeps the development of every element of the web app focused on the user experience first.
* *Planning*
   The initial stages where a specific element (e.g. a block of code, a server, etc.) is being considered for implementation.
* *In Progress*
   Once the element has had any code written for it/exists in any way, it is placed in the 'in progress' list.
* *Testing*
   Once the element has been created, it moves to the 'testing' list, where its functionality is tested.
* *Finished*
   Any element that is considered to be finished (i.e. works according to its specification) lives in this list.

## Risk Assessment
The risk assessment for this project can be found in full here: https://drive.google.com/file/d/1TTOwWYVql7eh4ftqLLOEpV-zif4iTCNM/view?usp=sharing

Here's a quick screenshot:

![RiskAssessment][https://imgur.com/a/UymDp8r]

## Testing
pytest is used to run unit tests on the app. These are designed to assert that if a certain function is run, the output should be a known value. Jenkins produces console outputs (pictured below) that will inform the developer how many tests the code passed and which tests they failed.

![pytestconsole][pytestconsole]

pytest also produces a coverage report to show how much of the code in the app has been successfully tested. Jenkins automatically moves this report to the 'templates' folder so that it can be navigated to in a browser, as shown in the picture below.

![coverage][https://imgur.com/a/XkVbvEv]

## Front-End Design
The front-end of the app is rudimentary at this stage, as the front-end is built purely with very simple HTML. It is largely functional and stable, however.

When the user navigates to the URL, they are directed to the home page:

![homeloggedout][homeloggedout]

They are then able to log in or register an account:

![signup][signup]

![login][login]

Once they are logged in, they now have access to the 'Enter Observation' page and their account page:

![homeloggedin][homeloggedin]

Navigating to the 'Enter Observation' page allows them to post an observation and optionally tag up to two other observers, which will appear at the top of the home page:

![enterobservation][enterobservation]

![homenewobservation][homenewobservation]

Navigating to the 'Account' page allows them to view their account details, update them and delete the account if they so desire. Deleting an account will also delete any observation they are associated with:

![account][account]

## Known Issues
There are a few bugs with the current build of the app:
* If a user attempts to change their email to another email that already exists in the database, the app will inexplicably delete the account entirely
* Certain errors do not appear on the front end when they should, for example: if the user inputs incorrect login information, they should receive an 'Incorrect Username' or 'Incorrect Password' warning – instead the page merely reloads

## Future Improvements
There are a number of improvements I would like to implement (outside of current bugs):
* Implementation of the stars and constellation database to allow you to tag these celestial objects in observations
* Allow the user to tag an indefinite number of users in an observation, rather than a maximum of two
* Filter observation posts by user, date, location, etc.
* Aesthetic overhaul, to make the front-end both more appealing *and* more functional
   * The aesthetics of an interface are important for the functionality of a web app, insofar as a user can only use functionality that they understand. Confusing aesthetic design will obscure the functionality of the app
   * This would be implemented using CSS, the easiest approach being with Bootstrap
* Implementation of other solar system objects that require realtime updates, e.g. planets whose locations in the sky are always changing
   * This would probably be best achieved by referring to another publicly-available database
* Users can customise their accounts more with profile pictures, add other users as friends, change the colour palette of the website, etc.

## Authors
Harry Volker

[erd1]: https://i.imgur.com/p9wji5S.png
[ci]: https://i.imgur.com/2G7joFp.png
[riskassessment]: https://i.imgur.com/btY8HRY.png
[coverage]: https://i.imgur.com/WDaANiD.png
[pytestconsole]: https://i.imgur.com/qaa3uzp.png
[trello]: https://i.imgur.com/etDOlwa.png
[buildstages]: https://i.imgur.com/ba7ntAo.png
[homeloggedout]: https://i.imgur.com/91NbyWE.png
[signup]: https://i.imgur.com/71f9E6y.png
[login]: https://i.imgur.com/vzwaTtv.png
[homeloggedin]: https://i.imgur.com/F4eXJKR.png
[enterobservation]: https://i.imgur.com/WsBmL6k.png
[homenewobservation]: https://i.imgur.com/NHxV8Gi.png
[account]: https://i.imgur.com/oXDX1y3.png
