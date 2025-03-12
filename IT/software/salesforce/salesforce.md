# [Salesforce CLI](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop)

**Salesforce CLI** (Command Line Interface) is a command-line tool provided by Salesforce.

## Install Salesforce CLI

- **Windows**

    - [Download and install **Salesforce CLI** from the official website.](https://developer.salesforce.com/tools/salesforcecli)

    - Confirm that the CLI is correctly installed and up to date.

        ```bash
        sf update
        ```

- **Linux**

    - Install the **npm** package manager.

        ```bash
        sudo apt update
        sudo apt install npm -y
        ```

    - Install the **Salesforce CLI** using **npm**.

        ```bash
        sudo npm install -g @salesforce/cli
        ```

- Check the version.

    ```bash
    sf -v
    ```

- Update the CLI.

    ```bash
    sf update
    ```

- VS Code Extension

    - Install the **Salesforce Extension Pack (Expanded)** extension in **VS Code**.
    - Press **Ctrl+Shift+P** in VS Code to open the command palette, type `SFDX`, and you can select commands provided by the Salesforce extensions.
    - If you can't find the command in the command palette, try to disable and then re-enable the extension.

- JDK

    - Some features of the extension require JDK support, so you need to install JDK. For details, refer to the **Java Notes**.

    - [Configure the full path to the Java runtime for the Apex server:](https://developer.salesforce.com/docs/platform/sfvscode-extensions/guide/java-setup.html)

        - Click the **Settings** button in the bottom-left corner.

        - Search for **apex**.

        - Select the **Salesforcedx-vscode-apex > Java: Home** tab. Then type the following path:

            ```
            C:\\Program Files\\Java\\jdk-21
            ```

# [Developer Console](https://trailhead.salesforce.com/content/learn/modules/developer_console)

The **Developer Console** is a web-based IDE provided by Salesforce.

- Workspace

[What you can do with Developer Console:](https://trailhead.salesforce.com/content/learn/modules/developer_console/developer_console_source_code)

- Execute an Apex Class
- Create an Aura Component
- Create Visualforce Pages and Components
- Create a Visualforce Page

## [Debug Logs](https://trailhead.salesforce.com/content/learn/modules/developer_console/developer_console_logs)

# Organization

## Org Basics

In Salesforce, an **Organization** (**Org**) refers to a **complete Salesforce environment**. An Org can be either a **production environment** or a **non-production environment**, and it includes its own **data, users, features, configurations, and customizations**.

Salesforce provides different types of Orgs, including:

- **Trailhead Playground**: Learning ENV.
- **Developer Edition**: Dev ENV.
- **Sandbox (Partial/Full Copy)**: Test ENV with production data.
- **Scratch Org**: Temporary ENV for DevOps.
- **Preview Sandbox**: Test upcoming releases in advance.
- **Production**: Production ENV.

## [Trailhead Playground](https://trailhead.salesforce.com/content/learn/modules/trailhead_playground_management)

### TP Basics

**Trailhead Playground** (**TP**) is a Salesforce-provided, **dedicated learning environment** designed for hands-on practice. 

- **Purpose**: Primarily used for Trailhead courses, challenges, and experiments.
- **Pre-configured**: Some components required by Trailhead courses are pre-installed.

- **Free**: Multiple TP instances can be created for free, with no time limits.
- **Limitations**: Some advanced features (e.g., API access) may be restricted.

### [Create a TP](https://trailhead.salesforce.com/content/learn/modules/trailhead_playground_management/create-a-trailhead-playground)

- **About language**: If you're using Trailhead in a language other than English, make sure that your playground is set to the same language as the hands-on challenge. Otherwise you may run into issues passing challenges.

- Open the **Trailhead** website.
- Click the **profile icon** in the top-right corner.
- Select **Hands-On Orgs**.
- Click **Create Playground**.

### [Get TP Username and Password](https://trailhead.salesforce.com/content/learn/modules/trailhead_playground_management/get-your-trailhead-playground-username-and-password)

- **Notice**: The username and password here are specifically for TP, not for Trailhead.
- Accessing TP from within Trailhead does not require a username or password. 
- Accessing TP from outside Trailhead (e.g., **Salesforce CLI** and **VS Code**) requires a username and password.
- Launch a TP.
- Click the **Get Your Login Credentials** tab. Here you can see your **current TP username**. 
- Click **Reset My Password**. This sends an email to the address associated with your username.
- Click the link in the email.
- Enter a new password, confirm it, and click **Change Password**. 

## Developer Edition

### DE Basics

**Developer Edition** (**DE**) is a Salesforce-provided,  **development environment** designed for developers. 

# Objects

## Objects Basics

In Salesforce, **Objects** are **database tables** that store specific types of data. Each object consists of **fields** (columns) and **records** (rows),

Salesforce supports various types of objects, including:

- **Standard Objects**
- **Custom Objects**
- **External Objects**
- **Platform Events**
- **BigObjects**

## Standard Objects

**Standard Objects** in Salesforce are pre-built, out-of-the-box objects to help manage common business processes. 

## Custom Objects

**Custom Objects** in Salesforce are user-defined objects created to store data that is specific to an organization's business needs. 

### Create a Custom Object

- Select an Org.
- **Setup** > **Object Manager**
- **Create** > **Custom Object**
    - For **Label**, enter `<label_name>`. Notice that the **Object Name** and **Record Name** fields auto-fill.
    - For **Plural Label**, enter `<label_names>`.
    - Select the checkbox **Launch New Custom Tab Wizard after saving this custom object**.
    - Leave the rest of the values as default and click **Save**.

- **New Custom Object Tab**
    - Click the **Tab Style** field and select a style you like.
    - Click **Next**, **Next**, and **Save**.


## [Object Relationships](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

There are two main types of object relationships: **lookup** and **master-detail**.

### Lookup Relationship

A **Lookup Relationship** in Salesforce is a type of relationship where one object can be linked to another object, but it does not require the dependent object to be strictly tied to the primary object. 

Similar to a **foreign key**, it allows a non-strict relationship between objects. For example, a **Contact** can be related to an **Account**, but the **Contact** can still exist independently.

#### Create a Lookup Relationship

- Select an org and create a custom object.
- From **Setup**, go to **Object Manager** | **<object_name>**.
- In the sidebar, click **Fields & Relationships**. 
- Click **New** in the top right.
    - For **data type**, Choose **Lookup Relationship** and click **Next**.
    - For **Related To**, choose a right one, and click **Next**.
    - For **Field Name**, enter Contact, then click **Next**.
    - Click **Next**, **Next**, **Next**, and **Save**.

### Master-Detail Relationship

A **Master-Detail Relationship** in Salesforce is a type of relationship where one object (the **Master**) controls another object (the **Detail**). The **Detail** object is highly dependent on the **Master** object, and its existence is tied to the **Master**. If a **Master** record is deleted, the associated **Detail** records are also deleted automatically.

#### Create a Master-Detail Relationship

- Select an org.
- Create the 1st custom object **<1st_object_name>**.
    - Create a field.
    - Create a record.
- Create the 2nd custom object **<2nd_object_name>**.
- Create a **lookup relationship**.
- Create a **Master-Detail Relationship**.
    - From **Setup**, go to **Object Manager** | **<object_name>**.
    - In the sidebar, click **Fields & Relationships**. 
    - Click **New** in the top right.
    - For **data type**, Choose **Master-Detail Relationship** and click **Next**.
    - For **Related To**, choose **<1st_object_name>**, and click **Next**.
    - For Field Name, enter `Property` and click **Next**.
    - Click **Next**, **Next**, and **Save**.
- Contact **<2nd_object_name>** with **<1st_object_name>**.
    - From the **App Launcher** find and select **Sales**.
    - Click the **<1st_object_name>** tab in the navigation bar. 
    - Click **Related**. You’ll see **<2nd_object_name>** (0) in the Related tab.
    - Click **New**. Enter a name for **Favorite Name**, then click **Save**.

# Tabs

## [Create a Tab](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_custom_objects?trail_id=force_com_dev_beginner)

# Fields

## Fields Basics

In Salesforce, **Fields** (columns) are the individual pieces of data that make up a record in an object.  Each field represents a specific type of information, such as text, numbers, dates, or relationships with other objects. Fields are used to store and display data, and they define the structure of an object.

**Standard Fields**: These are pre-defined fields provided by Salesforce for standard objects like **Account**, **Contact**, and **Opportunity**. Examples include **Name**, **Created Date**, and **Phone**.

**Custom Fields**: Users can create custom fields for both standard and custom objects to capture specific information that the out-of-the-box fields do not cover.

In the **Field Name** column, for example, `Price__c`, the `__c` suffix is an easy way to identify a custom field.

## Create a Field

- Select an org and create a custom object.
- From **Setup**, go to **Object Manager** | **<object_name>**.
- In the sidebar, click **Fields & Relationships**. 
- Click **New** in the top right.
    - For **data type**, select the right one, Then click **Next**.
    - Fill out **Field Label** field, and **Field Name** field auto-fill.
    - Check the **Required** box.
    - Click **Next**, **Next** again, and then **Save**.
- Create Records
    - From the **App Launcher** find and select **Sales**.
    - Click the **<object_name>** tab in the navigation bar. 
    - Click **New** in the top corner.
    - Enter a name and price for the Object and click **Save**.

# Records

# [Lightning Web Components](https://trailhead.salesforce.com/content/learn/modules/lightning-web-components-basics)

**Lightning Components** is a framework for developing mobile and desktop apps.

# [Lightning Apps Builder](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_apps?trail_id=force_com_dev_beginner)

# [Layout Editor](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)

# [List Views](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_list?trail_id=force_com_dev_beginner)

## Create a List View

- **App Launcher** > **Sales** > **Accounts** > **New**

    ![image-20250305183252478](assets/image-20250305183252478.png)

- Name the list `Channel Customers`.

- Select **All users can see this list view**.

- Click **Save**.

- Set up some filters.

    - Click **Add Filter**.
    - From the **Field** dropdown menu, select **Type**.
    - Select the **equals** operator.
    - For Value, select **Customer - Channel**, then click **Done** and **Save**.
    - Add another filter where **Billing State/Province** equals **WA,OR,CA**.

## Create a List View Chart

- From the **Sales** app, click the **Opportunities** tab.

- Use the dropdown menu (![img](assets/fdb2f0c6d4ef6479100d7f00ac06136f_i.27.jpg)) to select the **All Opportunities** list view.

- Click ![list view charts icon](assets/6ca3d60bc72bc7d3f259dd3320c64cdf_i.28.jpg). 

- In the Charts panel that appears, click ![list view charts gear icon](assets/22d51ae434c5c03addbc4f8853f34cfb_i.29.jpg) and select **New Chart**.

- Name the chart `Pipeline Total Value` and give it these parameters.

    - Chart Type: **Donut Chart**

    - Aggregate Type: **Sum**

    - Aggregate Field: **Amount**

    - Grouping Field: **Account Name**

- Click **Save**.

# [Compact Layouts](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_compact_layouts?trail_id=force_com_dev_beginner)

# [Formulas](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic?trail_id=force_com_dev_beginner)

## [Formulas](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/formula_fields?trail_id=force_com_dev_beginner)

### Standard

- Case sensitive.
- Whitespace and line breaks don’t matter.

### Creat Formulas

- **Setup** > **Object Manager** > **Opportunity** > **Fields & Relationships** > **New** > **Formula**
- In **Field Label**, type `Days to Close`. Notice that **Field Name** populates automatically.
- Select the type of data you expect your formula to return.
- Click **Next** until arrive at the formula editor!
- Edit your formula, then click the check button.
-  **Put your new formula field in a report.** 
    - From the **App Launcher**, find and open **Reports** and click **New Report**.
    - Enter **Opportunities** in the Search Report Types... field. Select **Opportunities** and click **Start Report**. Your opportunity appears in the Report Preview panel.
    - Make sure **Update Preview Automatically** is enabled.
    - In the Add column... field on the left side of the page, enter `Days to Close`. 
- Find the field `Days to Close`: **App Launcher** > **Opportunities** > **Details**

## [Roll-Up Summary Fields](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/roll_up_summary_fields?trail_id=force_com_dev_beginner)

Roll-up summary fields calculate values from a set of related records.

Roll-up summary fields are based on the master side of a master-detail relationship. 

### Creating the Summary Field

- From Setup, open **Object Manager** and click **Account**.
- On the left sidebar, click **Fields & Relationships**.
- Click **New**.
- Choose the **Roll-Up Summary** field type, and click **Next**.
- For Field Label, enter `Sum of Opportunities` and click **Next**.
- The Summarized Object is the detail object that you want to summarize. Choose **Opportunities**.
- Choose the **SUM** Roll-up type and choose **Amount** as the Field to Aggregate. If you're unable to see Amount in Field to Aggregate, disable the Advanced Currency Management in your Currency Setup.
- Click **Next**, **Next**, and **Save**.

##  [Validation Rules](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/validation_rules?trail_id=force_com_dev_beginner)

Validation rules verify that data entered by users in records meets the standards you specify before they can save it. 

When the validation rule returns a value of "True", this confirms that the data entered by the user contains an invalid value. 

### Creating a Validation Rule

1. From Setup, go to **Object Manager** and click **Account**.
2. In the left sidebar, click **Validation Rules**.
3. Click **New**.
4. Enter the following properties for your validation rule:
    1. Rule Name: `Account_Number_8_Characters`
    2. Error Condition Formula: `LEN( AccountNumber) <> 8`
5. Error Message: `Account number must be 8 characters long.`
6. To check your formula for errors, click **Check Syntax**.
7. Click **Save** to finish.

# [Flow Builder](https://trailhead.salesforce.com/content/learn/modules/flow-basics/meet-flow-builder?trail_id=force_com_dev_beginner)

## Creat a Flow Builder

- To get to Flow Builder, go to Setup, enter `Flows` in the Quick Find box, and select **Flows**. 
- To create a flow, click **New Flow**. Then select **Start from Scratch** and click **Next**.
- Select a flow type, click **Create**.

## Layout

<img src="assets/image-20250311220230555.png" alt="image-20250311220230555" style="zoom:50%;" />

- **Toolbox (1)** : The toolbox lists the elements and resources you’ve built in your flow. You can also create resources such as variables, formulas, and choices to use in your flow.
- **Canvas (2)** : The canvas is the working area.
- **Button Bar (3)**: Provide some tools.

## Building Blocks

- Flows use three building blocks: elements, connectors, and resources.

    <img src="assets/image-20250311221030163.png" alt="image-20250311221030163" style="zoom:50%;" />

### Elements

- **Elements** are nodes on the canvas that make things happen. To add an element to the canvas, click ![Add element](assets/13f5207391f198a601856fce8a8a6280_kix.10ac7o3ovpkx.jpeg).
- Each element is a step that tells the flow what to do, and each type of element does something different. 
- Think of flow elements as three types.
    - Interaction
    - Data
    - Logic

### Connectors

- **Connectors** are lines on the canvas that define the path the flow takes when it runs.

### Resources

- **Resources** are containers that don’t appear on the canvas, but are referenced by the flow’s elements. Each resource contains a value or a formula that resolves to a value.

## [Variables](https://trailhead.salesforce.com/content/learn/modules/flow-basics/learn-about-flow-variables)

- **Variable** is a kind of **Resources**.

- **Text**: A string of letters, numbers, and characters.
- **Number, Currency:** A numerical value.
- **Boolean**: A true or false value.
- **Date, Date/Time**: A specially formatted value that indicates a specific date, or a specific time on a specific date. 
- **Record**: All of the values in a Salesforce record, stored together in a single variable.
- ...

### Create a Variable

- From Setup, enter `Flows` in the Quick Find box and then click **Flows**.

- Click **New Flow**.

- Make sure **Start from Scratch** is selected, and click **Next**.

- Select **Screen Flow** and click **Create**.

- Click ![Toggle Toolbox](assets/1121645553b3bb884e333a7e2271ec97_kix.im3gqi7i1ify.jpeg) to display the Toolbox.

- Click **New Resource**. 

- For Resource Type, select **Variable**.

- Enter an API name and description for your variable.

    <img src="assets/image-20250311224935231.png" alt="image-20250311224935231" style="zoom:50%;" />

- For Data Type, select **Text**.

## [Constants](https://trailhead.salesforce.com/content/learn/modules/flow-basics/learn-about-flow-variables)

- **Constant** is a kind of **Resources**.

# Project

## [Create a Project](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop)

- **Precondition**

    - Create a new TP.

    - Install Salesforce CLI.

    - Install Node.js.

- Press **Ctrl+Shift+P** in VS Code to open the command palette, and type **SFDX**.

    - Select **SFDX: Create Project**.
    - Select **Standard**.
    - Type the project name and press **Enter**.
    - Set the project location.

- **Authorize**

    - Press **Ctrl+Shift+P** in VS Code to open the command palette, and type **SFDX: Authorize an Org**.
    - Select **Production** and type the organization alias **myDevOrg**. Then press **Enter**.
    - A Webpage will pop up for login.
    - **Notice**: Type the username and password of **TP**.

- Ways to open the a organization

    - **Command Line**：Run the command in the terminal at the project's root directory.

        ```bash
        sf org open
        ```

    - **VS Code**

        <img src="assets/image-20250302212052512.png" alt="image-20250302212052512" style="zoom:50%;" />

- Navigate to the project's root directory in the terminal and run the command below to install the project dependencies.

    ```bash
    npm install
    ```

# Package

## [Install a Package](https://trailhead.salesforce.com/help?article=Installing-a-package-or-app-to-complete-a-Trailhead-challenge)

