# Lab Report Template for CIS411_Lab1

Course: Messiah College CIS 411, Fall 2018

Instructors: [Joel Worrall](https://github.com/tangollama) & [Trevor Bunch](https://github.com/trevordbunch)

Name: Ben Underwood

GitHub: [benunderw](https://github.com/benunderw)

Collaborators: Ben Underwood, Kira Fernández, Sam Mahan


# Step 0: Reviewing Architectural Patterns
See the [lecture / discussion](https://docs.google.com/presentation/d/1nUcy63FWPFYO3OJmERJpMjEtdaFtaIBbuUkpmNRVRas/edit#slide=id.g45345bd5ea_0_136) from CIS 411. You'll need to be familiar with the content from this lecture to complete this assignment.

Note: you are free to work with classmates on this assignment. _Good architecture is born out of collaboration - not reclusive mad-scientist behavior._ However, if you work with colleagues:

1. You must specifically note your collaborators by name at the top of your report.
2. You may not completely copy each others work (diagrams and descriptions, even if your solutions are identical).

# Step 1: MVC Architecture
Review the proposals for the Serve Central project. Let's imagine that the project has been granted (relatively) unlimited resources if they can deliver a version 1 release in 120 days. As a result, the team decides to implement an MVC architecture for its version 1 release, delivering functionality through a [responsive web application](https://en.wikipedia.org/wiki/Responsive_web_design). 

Based on the [this](https://docs.google.com/presentation/d/1UnU0xU0wF1l8pAB8trtLpdM0yuskx66jTFJzd64nsjU/edit#slide=id.g439b9c6866_2_53) and [this](https://docs.google.com/presentation/d/1-VZfAFoBVr6ijNepKAtRA7JoAQsV2Jlbf2l1WPDMhI0/edit) presentation:

1) Document two use cases of your choosing

| Use Case #1 | |
|---|---|
| Title | Find service opportunities |
| Description / Steps | Load more information about that opportunity in any view |
| Primary Actor | The user of the client application *tron legacy soundtrack plays* |
| Preconditions | 1. Open the app<br>2. Map view loads automatically with service opportunities represented as pins. The user can choose a different view based on their preferences. (List or Map View) <br>3. Choose an opportunity from available options|
| Postconditions | Tooltip/modal with more information about the service opportunity |

| Use Case #2 | |
|---|---|
| Title               | Sign up for a service opportunity |
| Description / Steps | User fills and submits signup form, the contents of which is saved in a databse |
| Primary Actor       | The user of the client application |
| Preconditions       | 1. Service opportunity information is loaded <br>2. User presses the signup link |
| Postconditions      | Form data is saved in a database |


2) Highlight a [table](https://www.tablesgenerator.com/markdown_tables) of at least **four models, views, and controllers** needed to produce this project.

| Model | View | Controller |
|---|---|---|
| Opportunity Data | Map View     | Form Controller |
| User Data        | List View    | Map Controller  |
| Analytics Data   | Profile View | Profile Controller |
| Form Data        | Form View    | List Controller |

3) Generate and [embed](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#images) at least one diagram of the interaction between an Actor from the Use Cases, and one set of Model(s), View(s), and Controller(s) from the proposed architecture, including all the related / necessary services (ex: data storage and retrieval, web servers, container tech, etc.)

_Note: You are free to use any diagraming tool and framework that you want as long as it clearly communicates the concept. I typically use a UML System Use Case or [UML Sequence Diagram](https://www.uml-diagrams.org/index-examples.html).  If you do not have a preferred diagramming tool: [draw.io](http://draw.io) or [lucidchart](http://lucidchart.com) are good cloud-based options._

![Use case #1](https://i.imgur.com/xu5Pa8n.png)

![Signup Form MVC Structure](https://i.imgur.com/VFRirm7.png)

# Step 2: Enhancing an Architecture
After an initial release and a few months of operation, Serve Central encounters a tremendous growth opportunity to extend their service and provide a volunteer recuitment and management interface to __four__ of the primary volunteer entities in the United States. As such, a reevaluation of the architecture is required, one that allows:

1. Third-party services to both input and retrieve data from the Serve Central model/datastore. (For instance, receiving volunteer opportunities from United Way chapters across the country.)
2. Building organization-specific interfaces on top of the Serve Central business and data logic. (For instance, allowing the registration services of Serve Central to be embedded in the website of local churches, [ah-la Stripe embedding](https://stripe.com/payments/elements).)

To support these objectives:
1. What architectural patterns (either of those presented in class on based on your own research) are appropriate? Justify your response, highlighting your presumed benefits / capabilties of your chosen architecture(s) **as well as as least one potential issue / adverse consequence** of your choice.

One appropriate architectural pattern could be using GraphQL to query required event/user data, as well as for interfacing with external APIs (such as Facebook or LinkedIn). If there are a lot of websites interfacing with ServeCentral's data, GraphQL could help organize that data for other services' use. The benefits would include ease of access for data querying; the consequences might include having to maintain the API supporting GraphQL (which is developed by Facebook).

2. Using your preferred diagramming tool, generate a diagram of the new Serve Central architecture that supports these two new requirements.

![GraphQL Interface](https://i.imgur.com/c6eJWvb.png)

# Step 3: Scaling an Architecture
18 months into the future, Serve Central is experiencing profound growth in the use of the service with more than 100k daily, active users and nearly 1M event registrations per month. As a result, the [Gates Foundation](https://www.gatesfoundation.org/) has funded a project to build and launch a mobile application aimed at encouraging peer-to-peer volunteer opportunity promotion and organization. 

In addition to building a new mobile application interface, the grant requires that the project prepare for the following future needs:

1. Consuming bursts of 10k+ new volunteer opportunities per hour with a latency of less than 15 seconds between submitting an opportunity and it's availability in the registration service.

2. Supporting a volunteer and event data store that will quickly exceed 50TB of data

3. Allowing authorized parties to issue queries that traverse the TB's of data stored in your datastore(s).

4. Enabling researchers to examine patterns of volunteer opportunities as a way of determining future grant investments.

What archictural pattern(s) will you employ to support each of these needs? What will the benefits and consequences be? Why are changes needed at all? Justify your answers.

No changes are needed. We're perfect. -Kira Fernández

Serious answer: (1), (2), and (3) can be addressed with a load balancing system using technologies such as Kubernetes and Docker. Benefits include distributing the increased traffic to ServeCentral to lessen the load per server (controller) and handle higher loads in general. Drawbacks include higher costs/maintenance. 

(3) and (4) will require a customized controllers (using services like GraphQL) and views for the external users to easily interact with. 
