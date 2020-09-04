# Bookmark and url shortening

## Problem statement

Our organization is going through a digital transformation phase. During this journey, **we have created several digital  components across various platform**(like micro services, widgets, documentations, monitoring dashboards etc). 

The easiest way to have the references of all these components is through bookmarks. However, bookmarks has to be imported and exported inorder to share it with any one like a new joiner. In bookmarks, **you cannot detail more about what these bookmarks are about** by providing additional information through short description or an image(s) or customized icons(s). 

**Bookmarks are not centralized**. Even if you try to centralize it by exporting them and storing in a repository, every time an url is changed or added or removed all the people have to re-import those bookmarks from the centralized repository. It also becomes complex when you already have bookmarks and then importing which could result in overlapping.

It also becomes **hard when we want to share many such lengthy urls** such as kibana dashboard urls. A shorter url will become easy to share in this case.  


## Requirements and goals

Our system should meet the following requirements:

### Functional requirements

* User can generate short url's which will expire after a standard default timespan. User can also be able to specify the expiration date. This will help us solve the problem of generating tiny urls quickly and sharing it with others.

* User should be able to create cards representing the url where each card has a short title, brief description and a customizable picture. Default picture would be the favicon of the serving application. A sample pen sketch is as below:

    ![Sample Card](img/card.png)
    
    > :pushpin: NOTE: You are free to design the cards in your own way to better the user-experience. **THIS IS JUST A SKETCH TO ILLUSTRATE**.  

* User should be able to group cards in terms of tribes, feature teams, platforms or application. **This would be like a catalog**. User should be able to share the group urls. 

    ![Group Card](img/group-cards.png)

* Each card should be a short url with the re-direction to the original url. **This short url will have no expiration as it belongs to a group**. The generation of this short url should be dynamic and unique and could carry some contextual information too.

    _For example:_ Let us image we have a url

    > http://someapp:5601/app/kibana#/dashboard/target_new_prod_dashboard?_g=(refreshInterval:(display:Off,pause:!f,value:0),time:(from:now-7d,mode:quick,to:now))&_a=(filters:!(),options:(darkTheme:!f),panels:!((col:1,id:ogn-data-received-vs-ogn-data-saved,panelIndex:1,row:1,size_x:5,size_y:4,type:visualization),(col:1,id:missing-ogn-information,panelIndex:2,row:5,size_x:5,size_y:5,type:visualization),(col:6,id:distribution-of-new-production-types,panelIndex:3,row:1,size_x:4,size_y:8,type:visualization)),query:(query_string:(analyze_wildcard:!t,query:'*')),title:target_new_prod_dashboard,uiState:())

    |    Group Context      |            Example            |
    |:---------------------:|:-----------------------------:|
    | None                  | http://tiny/klsjd73           |
    | User                  | http://{paul}/klsjd73           |
    | Tribe                 | http://{tribe-name}/klsjd73     |
    | platform\application  | http://{ft-name}/klsjd73        |

* The creator of the group will be the admin(role) user after which s\he will be able to add one or more admin user who would have authority to make changes. Only admin user(s) can remove a user from admin role. At any point of time there must be at least one admin user for the group. 

* Admin user(s) of the group should be able to authorize a card to be displayed on the group, make changes like updating or delete card(s). Unless the admin user approves the card or its changes, it will not be displayed on the group page.

* A normal user i.e. not an admin user can suggest changes to an existing card. The changes are to be queued in order to be approved by the group's admin user(s).

* User should be able to share the group page enlisting all the cards of that group

* Admin user(s) should be able to import or export 

      
### Non-functional requirements

* The system should be highly available. This is required because, if our service is down, all the URL redirections will start failing.

* URL redirection should happen in real-time with minimal latency.

* Shortened links i.e. klsjd73 should not be guessable (not predictable).

* System should be maintainable, easy to adapt any new changes.

* Try to use the concept of [web components](https://www.webcomponents.org/introduction) or widgets. The cards need to be re-usable and support multiple browser with any underlying library or framework i.e.we can take the card\group and embed in an application or platform.

* All of the behaviours needs to be exposed as RESTful api's with [open api specification](https://swagger.io/specification/) documentation which can be tried with "Try out" in order to try out the api's

* **We strongly recommend you to set-up [CI\CD](#cicd) right from the beginning of the project**

### Extended requirements

- If you have any other ideas or features that could add more business value.

- Metrics: e.g. how many times a redirection happened? How many users are using your group ? etc

- Our service should also be accessible through REST APIs by other services.

- Any extra feature that can create business value(optional)

## Technology stack

### Java

* Backend
    - Language: Java or kotlin (AdoptOpenJDK 11 and above)
    - Framework: Spring, spring-boot, spring-cloud 
* Frontend
    - Language: Typescript or JavaScript
    - Framework: (P)React, Angular, Vue
* Database
    - MySQL, PostgreSQL, MongoDB, Inmemory

### .Net

* Backend
    - Language: C#
    - Framework: dotnet core (version 2 or 3), Aspnet.core
* Frontend
    - Language: Typescript or JavaScript
    - Framework: (P)React, Angular, Vue
* Database
    - MS SQL, PostgreSQL, MongoDB
    - DB Connectivity : Entiry Core or Daper(Do not use ADO.net)    

## What are you suppose to submit ?

- You will have to create your own organization and make your repositories private and use this for this hackathon. We recommend you to setup [CI\CD](#cicd) right from the start for each of your repository.
- All [functional](#functional-requirements), [non-functional](#non-functional-requirements) and [extended](#extended-requirements) requirements needs to be implemented and working.
- A design documentation satisfying both functional, non-functional and extended requirements with the data flow of various components involved in the form of markdown committed at [GitHub](https://github.com/)
- A pictorial representation of DB schema: tables and relationships if any
- A working code with widgets(web components) representing the cards
- RESTful api with [open api specification](https://swagger.io/specification/) url
- The links of ci\cd, quality and cloud hosting

> :pushpin: NOTE: We will let you know in advance if there are any other additional things we would require

## How are we planning to evaluate ?

### Documentation

We will be checking a lot of detailing about the solution for functional, non-functional and extended requirement along with options where ever applicable and why did you choose a specific solution from the various options. This will show how well you have understood the problem, how have you studied the various components and how did you evaluate a specific solution. Can you take a step ahead with [docsify](https://docsify.js.org/#/) and gh-pages?

- Does the document talk about how to build start, test, and deploy locally as well as through automated tools?
- Does the document talk about system design and the various components involved?
- Does the document talk about various technical choices and decisions made through [ADR](https://adr.github.io/)?


### RESTful API

We will be checking how well you have designed your RESTful api and how much of the global standardization have you adopted. Your APIs will be validated against swagger checker.

### Readable

We write code not for machines to understand but for another contributor to understand and contribute. Format them well with a definite code style like [google style guide](https://google.github.io/styleguide/).

### Testable

How well you have written tests with [test pyramid](https://martinfowler.com/bliki/TestPyramid.html). Are you following TDD or BDD approach? You commit will show what kind of approach you are following. The approach of TDD will generally include test along with production code. **TESTS ARE NOT FOR COVERAGE**.

### Commit and commit message

A good developer always makes incremental commits with [meaningful commit message](https://www.conventionalcommits.org/en/v1.0.0/) for helping other collaborators to back trace though commit message. **DO NOT JUST MAKE ONE COMMIT**.

### Quality

How do you automate the quality checks of your code and make the reports available in terms of violations and code coverage. Failing fast is one of the key aspect that helps in delivering a software in agile. How do you help in failing fast and help deliver quality code. 

### CI\CD

How have you automated your code to be compiled, tested, verified for quality and deployed. You would have to choose from the following options:
- Job runner: [TravisCI](https://travis-ci.org/) or [CircleCI](https://circleci.com/) for task runner
- Coverage report: [Codecov](https://codecov.io/) for test running and reporting coverage. Would be great if you can showcase for each commit or pull-request how you can run your coverage checks.
- Quality report: [Codacy](https://app.codacy.com/) for checking your code quality. Would be great if you can showcase for each commit or pull-request how you can run your quality checks.
- Kibana\Grafana dashboard for monitoring
- Cloud server: [Heroku](https://www.heroku.com/) or google cloud or AWS or Azure for cloud. Use trial option. 

## Contacts

Connect with us through [![Gitter](https://badges.gitter.im/engineering-stream-hackathon/community.svg)](https://gitter.im/engineering-stream-hackathon/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)