# Salesforce Platform Basics

## [Install the Dreamhouse App](https://trailhead.salesforce.com/content/learn/modules/starting_force_com/starting_intro?trail_id=force_com_dev_beginner)

## [Create a Field](https://trailhead.salesforce.com/content/learn/modules/starting_force_com/starting_intro?trail_id=force_com_dev_beginner)

# Platform Development Basics

## Get Started with the Salesforce Platform

### [Install the Dreamhouse App](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/get-started-with-the-salesforce-platform-01?trail_id=force_com_dev_beginner)

- Install the **Dreamhouse** App again with the new Packge ID `04t3h000004bhxlAAA` in a new TP.

## [Develop Without Code](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/develop-without-code-01?trail_id=force_com_dev_beginner)

- Schema Builder

- Lightning Apps Builder

- Flows (Low-code)

## [Code with Salesforce Languages](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/code-with-salesforce-languages-01?trail_id=force_com_dev_beginner)

- Lightning Web Component Framework
- Apex
- Node.js

## [Extend the Salesforce Platform](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/extend-the-salesforce-platform-01?trail_id=force_com_dev_beginner)

Introduce how to Extend the Salesforce Platform:

- API
- Platform Events
- Heroku
- Einstein

# Get Started with Salesforce Development

## [Get Ready to Develop](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner)

- Install Salesforce CLI.
- Install Salesforce Extension Pack.
- Creat a new TP.

- Create a New Salesforce Project

## [Create a Data Model Using Clicks](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/create-a-data-model-using-clicks?trail_id=force_com_dev_beginner)

- Create a **House** Custom Object with uploading a CSV file.
- Create an App **Dreamhouse**.

- Retrieve **Metadata** from Salesforce to the Local Project.

## [Write Business Logic in Apex](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/write-business-logic-in-apex?trail_id=force_com_dev_beginner)

- Create and Deploy the Apex Class

## [Build a Reusable UI Component with Lightning Web Components](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/build-reusable-ui-component-with-lightning-web-components?trail_id=force_com_dev_beginner)

- Create and Deploy a Lightning Web Component
- Add the Component to the App Home

# Quick Start: Tour the Sample App Gallery

## [Get to Know the Sample Gallery](https://trailhead.salesforce.com/content/learn/projects/quick-start-tour-the-sample-app-gallery/get-to-know-the-sample-gallery?trail_id=force_com_dev_beginner)

- Sample Apps in GitHub: [github.com/trailheadapps](https://github.com/trailheadapps)

## [Learn About Sample App Tooling](https://trailhead.salesforce.com/content/learn/projects/quick-start-tour-the-sample-app-gallery/learn-about-sample-app-tooling?trail_id=force_com_dev_beginner)

- Project Configurations: sfdx-project.json
- Code Quality Tool Setup: npm
- Unit Testing Configuration
- Automated Code Formatting Configuration
- Ignore files
- GitHub Actions: CI/CD
- Open Source at Salesforce: [Code Samples and SDKs](https://developer.salesforce.com/code-samples-and-sdks)

# Data Modeling

## [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)

- Get to Know Objects
- Creat a new TP: **Optimize Customer Data with Standard and Custom Objects**
- Create a Custom Object: **Property**
- Get to Know Fields
- Create a Custom Field: **Price**
- Create a Record: **Jerry's house**

**Challenge**: 

- Create a custom object
    - Label: **Offer**
    - Object Name: `Offer`
    - Record Name: **Offer Name**
    - Data Type: **Auto Number**
    - Display Format: **OF-{0000}**
    - Starting Number: **1**
- Create a custom currency field on the Offer object
    - Data Type: **Currency**
    - Field Label: **Offer Amount**
    - Field Name: `Offer_Amount`
- Create a custom date field on the Offer object
    - Data Type: **Date**
    - Field Label: **Target Close Date**
    - Field Name: `Target_Close_Date`

## [Create Object Relationships](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

- Create a Custom Object: **Favorite**
    - Use the TP you created in the previous unit: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
- Create a Lookup Relationship: **Contact**
- Create a Master-Detail Relationship: **Property**
- Add a Favorite Property: Add a detail record **Jerry's house - Related**.

**Challenge**:

Create relationships for the Offer object

The object you created for the previous challenge is pretty handy. Imagine how much more useful it would be if brokers could specify which client made an offer and which property the client wants to buy. Add two relationships to the Offer object so brokers can capture this data in Salesforce. Create a Master-Detail relationship with the Property object and a Lookup relationship with the Contact object.

Even if you're completing this module as part of the Admin Beginner trail, be sure you use the new Trailhead Playground you created in the previous unit.
**Before You Start:**

- Create the **Property** object as described in the previous unit.

**Challenge Requirements:**

- Create a custom Master-Detail field on the Offer object
    - Data Type: **Master-Detail**
    - Related To: **Property**
    - Field Label: **Property**
    - Field Name: `Property`
- Create a custom Lookup Relationship field on the Offer object
    - Data Type: **Lookup Relationship**
    - Related To: **Contact**
    - Field Label: **Contact**
    - Field Name: `Contact`

## [Work with Schema Builder](https://trailhead.salesforce.com/content/learn/modules/data_modeling/schema_builder?trail_id=force_com_dev_beginner)

- Based on the previous unit.
    - Learning
    - Challenge: the object **Offer**
- See Your Data Model in Action: **Schema Builder**
- Create an Object with Schema Builder. Any Name: **Object - Schema Builder**
- Create Fields with Schema Builder. Any Name: **Email - Schema Builder**

# Lightning Experience Customization

## [Set Up Your Org](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_custom_objects?trail_id=force_com_dev_beginner)

- Continue the TP in previous unit: **Optimize Customer Data with Standard and Custom Objects**
- Create a Custom Object: **Energy Audit**
- Create a Custom Object Tab
- Create many Custom Fields
- Create many Energy Audit Records
- Enable Feed Tracking
- Challenge: The challenge is the same as the learning.

## [Create and Customize Lightning Apps](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_apps?trail_id=force_com_dev_beginner)

- What Is a Lightning App?
- Meet the Lightning Experience App Manager
