---
title: trailhead-sample-beginner
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - code-language
  - salesforce
---

- Summary for Trailhead: [Developer Beginner](https://trailhead.salesforce.com/content/learn/trails/force_com_dev_beginner)
- Summary for Trailhead: [Build an Event Registration App](https://trailhead.salesforce.com/content/learn/projects/build-an-event-registration-app)

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
- What’s the Visible in Lightning Column About?
- Create a Lightning App: **Energy Consultations**
- Tips for Creating Apps in Lightning Experience

## [Create and Customize List Views](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_list?trail_id=force_com_dev_beginner)

- Create a List View: **Channel Customers**
    - Set up some filters.
- Create a List View Chart: **Pipeline Total Value**
- Challenge
    - Create a List View: **High Probability Opportunities**

## [Customize Record Highlights with Compact Layouts](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_compact_layouts?trail_id=force_com_dev_beginner)

- Create a Compact Layout: **Energy Audit Compact Layout**
- **Challenge**: Create a Compact Layout: **New Oppty Compact Layout**

## [Customize Record Page Components and Fields](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)

- Create a Custom Lightning Record Page
- Customize Related Lists
- Activate the Page
- View the Customized Page

## [Create Custom Buttons and Links](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_buttons_links?trail_id=force_com_dev_beginner)

- Introduce Buttons and Links
- Create a Custom List Button
- Create a Custom Detail Page Link
- Create a Custom Detail Page Button

## [Empower Your Users with Quick Actions](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_actions?trail_id=force_com_dev_beginner)

- Quick Actions
- Create an Object-Specific Action
- Add an Object-Specific Action to a Page Layout
- Create a Global Action
- Add a Global Action to the Global Actions Menu

# Formulas and Validations

## [Use Formula Fields](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/formula_fields?trail_id=force_com_dev_beginner)

- Create a new TP: **Use Formula Fields - learning**
- Example 1: Display an Account Field on the Contact Detail Page
- Example 2: Display the Number of Days Until an Opportunity Closes on a Report
- Debug Formulas
- More Examples

## [Implement Roll-Up Summary Fields](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/roll_up_summary_fields?trail_id=force_com_dev_beginner)

- Introduction to Roll-Up Summary Fields

- Creating the Summary Field

## [Create Validation Rules](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/validation_rules?trail_id=force_com_dev_beginner)

- Introduction to Validation Rules
- Creating a Validation Rule
- More samples

# Flow Builder Basics

## [Get Started with Business Process Automation](https://trailhead.salesforce.com/content/learn/modules/flow-basics/get-started-with-flows?trail_id=force_com_dev_beginner)

- [Two categories of automation](https://trailhead.salesforce.com/content/learn/modules/flow-basics/get-started-with-flows?trail_id=force_com_dev_beginner#the-power-of-automation)

## [Go with the Flow](https://trailhead.salesforce.com/content/learn/modules/flow-basics/go-with-the-flow-th?trail_id=force_com_dev_beginner)

- Some Important Flowcabulary
- Talking about when to use Flow

## [Meet Flow Builder](https://trailhead.salesforce.com/content/learn/modules/flow-basics/meet-flow-builder?trail_id=force_com_dev_beginner)

- The Flow Builder User Interface
- Continue the previous TP: **Use Formula Fields - learning**
- Flow Building Blocks
    - Elements
    - Connectors
    - Resources
- Keyboard Shortcuts

## [Learn About Flow Variables](https://trailhead.salesforce.com/content/learn/modules/flow-basics/learn-about-flow-variables?trail_id=force_com_dev_beginner)

- What Can I Store in a Variable?
- Create a Variable
- Things Similar to Variables
    - Constants
    - Formulas
    - Text Templates
- Challenge: Create some variables and a formular.
- Continue learning: [Build Flows with Flow Builder](https://trailhead.salesforce.com/content/learn/trails/build-flows-with-flow-builder) trail.

# Quick Start: Apex

- This's a inserted badge: [Quick Start: Apex](https://trailhead.salesforce.com/content/learn/projects/quickstart-apex)

## [Create an Apex Class](https://trailhead.salesforce.com/content/learn/projects/quickstart-apex/quickstart-apex-1)

- Creat a new TP: **Quick Start: Apex - learning**
- Create a Class: **OlderAccountsUtility**
- Add a Method: **updateOlderAccounts**
- Invoke and Test the Code
- Verify the Updated Accounts

# Apex Basics & Database

## [Get Started with Apex](https://trailhead.salesforce.com/content/learn/modules/apex_database/apex_database_intro?trail_id=force_com_dev_beginner)

- What is Apex?
- Development Tools
- Data Types Overview
- Apex Collections: List
- Apex Classes
    - Continue the previous TP: **Use Formula Fields -learning**
    - Save an Apex Class: **EmailManager**
    - Call a Method to Send an Email
    - Inspect Debug Logs
    - Call a Static Method

## [Use sObjects](https://trailhead.salesforce.com/content/learn/modules/apex_database/apex_database_sobjects?trail_id=force_com_dev_beginner)

## [Manipulate Records with DML](https://trailhead.salesforce.com/content/learn/modules/apex_database/apex_database_dml?trail_id=force_com_dev_beginner)

- Manipulate Records with DML
- Database Methods

## [Write SOQL Queries](https://trailhead.salesforce.com/content/learn/modules/apex_database/apex_database_soql?trail_id=force_com_dev_beginner)

- Create a new TP: **Write SOQL Queries**

## [Write SOSL Queries](https://trailhead.salesforce.com/content/learn/modules/apex_database/apex_database_sosl?trail_id=force_com_dev_beginner)

- **Prerequisites**: Insert something.
- Use the Query Editor

# Apex Triggers

## [Get Started with Apex Triggers](https://trailhead.salesforce.com/content/learn/modules/apex_triggers/apex_triggers_intro?trail_id=force_com_dev_beginner)

- Insert the previous modules
    - [SOQL for Admins](https://trailhead.salesforce.com/content/learn/modules/soql-for-admins)
        - Get Started with SOQL Queries
        - Create SOQL Queries in Apex Classes
        - Create Relationship Queries with Standard Objects
        - Create Relationship Queries with Custom Objects
            - Creat a new TP: **Create Relationship Queries with Custom Objects - challenge**
            - Install a Package: **DreamHouse** `04t3h000004mBpiAAE`
        - Use Bind Variables and Aggregate Functions
            - Bind Variables
            - Aggregate Functions
            - Group the Results of Aggregate Functions
            - Filter the Results of Aggregate Functions
    - [Developer Console Basics](https://trailhead.salesforce.com/content/learn/modules/developer_console)
        - Get Started with the Developer Console
        - Navigate and Edit Source Code
            - Create an Apex Class
            - Execute an Apex Class
            - What Are Lightning Components?
            - Create an Aura Component
            - Create Visualforce Pages and Components
        - Generate and Analyze Logs
            - View Logs in the Text Editor
            - Use the Log Inspector
            - Perspective Manager
            - Log Levels
        - Inspect Objects at Checkpoints
            - Set Checkpoints in Your Apex Code
            - Checkpoints Tab
        - Execute SOQL and SOSL Queries
            - What Is a SOQL Query?
            - What Is a SOSL Search?
- Trigger Syntax
- Creat a Trigger
- Trigger Events
- Context Variables
- Calling a Class Method in a Trigger
- Adding Related Records
- Using Trigger Exceptions

## [Bulk Apex Triggers](https://trailhead.salesforce.com/content/learn/modules/apex_triggers/apex_triggers_bulk?trail_id=force_com_dev_beginner)

- Operating on Record Sets

- Performing Bulk SOQL
- Performing Bulk DML

# Lightning Web Components Basics

## [Discover Lightning Web Components](https://trailhead.salesforce.com/content/learn/modules/lightning-web-components-basics/discover-lightning-web-components?trail_id=force_com_dev_beginner)

- Insert the previous modules: [Quick Start: Lightning Web Components](https://trailhead.salesforce.com/content/learn/projects/quick-start-lightning-web-components)
    - Set Up Your Salesforce DX Environment
        - Create a new TP: **Quick Start: Lightning Web Components**
        - Set Up Your Trailhead Playground
        - Get Your Trailhead Playground Username and Password
        - Install the Command Line Interface (CLI)
    - Set Up Visual Studio Code
    - Create a Hello World Lightning Web Component
        - Create a Salesforce DX Project
        - Authorize Your Trailhead Playground
        - Create a Lightning Web Component

## [Create Lightning Web Components](https://trailhead.salesforce.com/content/learn/modules/lightning-web-components-basics/create-lightning-web-components?trail_id=force_com_dev_beginner)

## [Deploy Lightning Web Component Files](https://trailhead.salesforce.com/content/learn/modules/lightning-web-components-basics/push-lightning-web-component-files?trail_id=force_com_dev_beginner)

- The Component Configuration File: **XML**

## [Handle Events in Lightning Web Components](https://trailhead.salesforce.com/content/learn/modules/lightning-web-components-basics/handle-events-in-lightning-web-components?trail_id=force_com_dev_beginner)

## [Add Styles and Data to a Lightning Web Component](https://trailhead.salesforce.com/content/learn/modules/lightning-web-components-basics/add-styles-and-data-to-a-lightning-web-component?trail_id=force_com_dev_beginner)

- CSS and Component Styling
- Applying Lightning Design System Styles

# Build an Event Registration App

## [Install the Package](https://trailhead.salesforce.com/content/learn/projects/build-an-event-registration-app/install-the-package)

- Create a new TP: **Build an Event Registration App**

## [Update the Data Model and Import Data](https://trailhead.salesforce.com/content/learn/projects/build-an-event-registration-app/update-the-data-model-and-import-data)

- Add a Custom Object: **Event Registration**
- Add Custom Fields for **Event Registration**
    - **Registration ID**
    - **Master-Detail Relationship**

## [Add Automation to Your App](https://trailhead.salesforce.com/content/learn/projects/build-an-event-registration-app/add-automation-to-your-app)

