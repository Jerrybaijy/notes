# Salesforce Tools

## Salesforce CLI

**Salesforce CLI** (Command Line Interface) is a command-line tool provided by Salesforce.

**Salesforce CLI command** should be executed in the root directory of project with **PowerShell**.

### [Install Salesforce CLI](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm)

- [**Windows**](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm#sfdx_setup_install_cli_windows)

    - Download and install [Salesforce CLI](https://developer.salesforce.com/tools/salesforcecli) from the official website.

    - Confirm that the Salesforce CLI is correctly installed and up to date.

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

- After the installation completes, restart your terminal tool or IDE to make sure Salesforce CLI is available.

- **Warning**: Salesforce CLI works best within the native Windows command prompt (cmd.exe) and the Microsoft Windows PowerShell. 


## Salesforce Extension Pack

**Salesforce Extension Pack** is a VS Code Extension.

- **Install Salesforce Extension Pack (Expanded)**

    - Install the **Salesforce Extension Pack (Expanded)** extension in **VS Code**.
    - Press **Ctrl+Shift+P** in VS Code to open the command palette, type `SFDX`, and you can select commands provided by the Salesforce extensions.
    - If you can't find the command in the command palette, try to disable and then re-enable the extension.

- **JDK**

    - Some features of the extension require JDK support, so you need to install JDK. For details, refer to the **Java Notes**.

    - [Configure the full path to the Java runtime for the Apex server:](https://developer.salesforce.com/docs/platform/sfvscode-extensions/guide/java-setup.html)

        - Click the **Settings** button in the bottom-left corner.

        - Search for **apex**.

        - Select the **Salesforcedx-vscode-apex > Java: Home** tab. Then type the following path:

            ```
            C:\\Program Files\\Java\\jdk-21
            ```

## [Developer Console](https://trailhead.salesforce.com/content/learn/modules/developer_console)

The **Developer Console** is a web-based IDE provided by Salesforce.

- Workspace

[What you can do with Developer Console:](https://trailhead.salesforce.com/content/learn/modules/developer_console/developer_console_source_code)

- Execute an Apex Class
- Create an Aura Component
- Create Visualforce Pages and Components
- Create a Visualforce Page

### [Debug Logs](https://trailhead.salesforce.com/content/learn/modules/developer_console/developer_console_logs)

# Organization

## Org Basics

In Salesforce, an **Organization** (**Org**) refers to a specific instance of Salesforce. An Org can be either a **production environment** or a **non-production environment**, and it includes its own **data, users, features, configurations, and customizations**.

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
- **Free**
    - Free, with no time limits.
    - Up to 10 TPs at a time.

- **Limitations**: Some advanced features (e.g., API access) may be restricted.

### [Create a TP](https://trailhead.salesforce.com/content/learn/modules/trailhead_playground_management/create-a-trailhead-playground)

- **About language**: If you're using Trailhead in a language other than English, make sure that your playground is set to the same language as the hands-on challenge. Otherwise you may run into issues passing challenges.

- Open the **Trailhead** website.
- Click the **profile icon** in the top-right corner.
- Select **Hands-On Orgs**.
- Click **Create Playground**.
- You‘ll receive an email when your new playground is ready. It may take a few minutes for your new playground to be created.

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

#### Custom Object

- Sample in Trailhead: [Create a Custom Object](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
- Create an Org.
- **Setup** > **Object Manager** > **Create** > **Custom Object**
- For **Label**, enter `Property`. Notice that the **Object Name** and **Record Name** fields auto-fill.
- For **Plural Label**, enter `Properties`.
- Select the checkbox **Launch New Custom Tab Wizard after saving this custom object**.
- Leave the rest of the values as default and click **Save**.
- **New Custom Object Tab**
    - Click the **Tab Style** field and select a style you like.
    - Click **Next**, **Next**, and **Save**.

#### Custom Object from Spreadsheet

- Sample in Trailhead: [Create a House Custom Object](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/create-a-data-model-using-clicks?trail_id=force_com_dev_beginner)
- Download and open [this spreadsheet](https://developer.salesforce.com/files/House.csv) and save it as **House.csv**.
- **Setup** > **Object Manager** > **Create** > **Custom Object from Spreadsheet**
- Click **Login With Salesforce**.
- Login with your username and password of your **org**.
- Click **Allow**. Then upload the **House.csv** file you downloaded.
- Salesforce automatically detects the fields and populates all its record data.
- Choose **House Name** as the Record Name field in the top right.
- Click **Next** and enter the following settings.
    - Label: `House`

    - Plural Label: `Houses`
    - API Name: `House`
- Click **Finish**. The House object is successfully created and data imported, all within minutes.
- Check the new object in the **Object Manager**.
- Check the records:
    - Select **Houses** From **App Launcher**.
    - Click **Recently Viewed**, then select **All Records** to view all of the records in the House object.

- There're some other fertures in the Trailhead sample:
    -  [Data Security](https://trailhead.salesforce.com/content/learn/modules/data_security)
    - REST API
    - [Salesforce APIs Postman collection](https://github.com/forcedotcom/postman-salesforce-apis)
    - [Salesforce Mobile app](https://www.salesforce.com/solutions/mobile/overview/)

- To work with the **House** object you just created, you need to create an **App** to allow easy navigation.
    - Refer to the sample of Trailhead: [Create an App](#Create an App)

## [Object Relationships](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

**Object Relationships** are a special field type that connects two objects together.

There are two main types of object relationships: **lookup** and **master-detail**.

### Lookup Relationship

A **Lookup Relationship** in Salesforce is a type of relationship where one object can be linked to another object, but it doesn't require the dependent object to be strictly tied to the primary object. 

Similar to a **foreign key**, it allows a non-strict relationship between objects. For example, a **Contact** can be related to an **Account**, but the **Contact** can still exist independently.

- Lookup Relationship from **Contact** to **Account** means: From **child** to **parent**.

    <img src="assets/image-20250326094031982.png" alt="image-20250326094031982" style="zoom: 67%;" />

- The relationship name is typically the plural form of the child object name.

- **Setup** > **Object Manager** > **Contact** > **Field & Relationships** > **Account Name**

    <img src="assets/image-20250326093815869.png" alt="image-20250326093815869" style="zoom:50%;" />

#### Create a Lookup Relationship

- Sample in Trailhead: [Create a Lookup Relationship](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

- Based on:

    - TP: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
    - Custom Object **Favorite**: [Create a Custom Object](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

- From **Setup**, go to **Object Manager** > **Favorite**.

- In the sidebar, click **Fields & Relationships**. 

- Click **New** in the top right.
    - For **data type**, Choose **Lookup Relationship** and click **Next**.
    - For **Related To**, choose **Contact**, then click **Next**.
    - For **Field Name**, enter `Contact`, then click **Next**.
    - Click **Next**, **Next**, **Next**, and **Save**.

- Check the new relationship field **Contact**.

    <img src="assets/image-20250319011834081.png" alt="image-20250319011834081" style="zoom:50%;" />

### Master-Detail Relationship

A **Master-Detail Relationship** in Salesforce is a type of relationship. The **Detail Record** is highly dependent on the **Master Record** , and its existence is tied to the **Master**. If a **Master record** is deleted, the associated **Detail records** are also deleted automatically.

#### Create a Master-Detail Relationship

- Sample in Trailhead: [Create a Master-Detail Relationship](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

- Based on:

    - TP: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
        - Custom Object: **Property**
        - Custom Field: **Price**
        - Custom Record: **Jerry's house**
    - Custom Object **Favorite**: [Create a Custom Object](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

- **Property** is the master and **Favorite** is the detail.

- From **Setup**, select **Object Manager**.

- Select the **detail** object **Favorite**.

- In the sidebar, click **Fields & Relationships**. 

- Click **New** in the top right.

    - For **data type**, Choose **Master-Detail Relationship** and click **Next**.
    - For **Related To**, choose the **master** object **Property**, then click **Next**.
    - Click **Next**, **Next**, and **Save**.

- Check the new relationship field **Property**.

    <img src="assets/image-20250319012633694.png" alt="image-20250319012633694" style="zoom:50%;" />

- Add a **Detail Record**

    - From the **App Launcher** select **Sales**.

    - Click the **Properties** tab in the navigation bar.

    - Click the name of a Property record: **Jerry's house**.

    - Click **Related** > **New**.

    - For **Favorite Name**, enter `Jerry's house - Related`, then click **Save**.

        <img src="assets/image-20250319022154054.png" alt="image-20250319022154054" style="zoom: 67%;" />

    - The detail record named **Jerry's house - Related** has been related to the master record **Jerry's house** of **Property**.

        <img src="assets/image-20250319023143015.png" alt="image-20250319023143015" style="zoom:50%;" />

    - The record **Jerry's house - Related** is showed in the object **Favorite**.

        <img src="assets/image-20250319023337761.png" alt="image-20250319023337761" style="zoom:67%;" />

# Fields

## Fields Basics

**Fields** are columns in object database tables. There are **Standard Fields** and **Custom Fields**

**Standard Fields**: These are **pre-defined** fields for standard objects, for example **Name**, **Created Date**, and **Phone**.

**Custom Fields**: Users can create custom fields for both standard and custom objects to capture specific information that the out-of-the-box fields don't cover.

- **Field Label**: Used on displays, page layouts, reports, and list views.
- **Field Name**: Used on custom links, custom s-controls, and the API.
    - For **custom object**, there's a `__c` suffix at the end of the field name. For example, `Price__c`.

## Create a Field

- Sample in Trailhead: [Create a Custom Field](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
- Based on the sample: [Create a Custom Object](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
- From **Setup**, locate to **Object Manager** > **Property**.
- In the sidebar, click **Fields & Relationships**. 
- Click **New** in the top right.
- For **data type**, select **Currency** and click **Next**.
- Fill out the following:
    - Type `Price` in the **Field Label** field, and **Field Name** field auto-fill.
    - Type `The listed sale price of the home.` in the **Description** field.
    - Check the **Required** box.
- Click **Next**, **Next** again, and then **Save**.
- You’ll see your new **Price** field in the list of **Property** fields.
- Notice that it says **Price\__c**. The “__c” part is an easy way to tell that a particular field is a custom field.

# Records

**Records** are the information the fields store.

<img src="assets/image-20250320013718967.png" alt="image-20250320013718967" style="zoom:50%;" />

- **record highlights** (1)
- **buttons and actions** (2)
- **Related** tab (3)
- **Details** tab (4)

## Create a Record

- Sample in Trailhead: [Create a Custom Record](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)

- Based on the sample:

    - [Create a Custom Object](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
    - [Create a Custom Field](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)

- From the **App Launcher** find and select **Sales**.

- Click the **Properties** tab in the navigation bar. 

- Click **New** in the top corner.

- Enter a name (**Jerry's house**) and price for the Object and click **Save**.

- You’ll see something like the following.

    <img src="assets/image-20250318231700387.png" alt="image-20250318231700387" style="zoom:50%;" />

## Check a Record

- From **App Launcher**, select the app the object showed on.
- Click the object tab.
- Open the All list view.
- Check the record.
- Detail refer to the sample: [Create a Custom Lightning Record Page](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)

# [Setup](https://trailhead.salesforce.com/content/learn/modules/starting_force_com/starting_tour?trail_id=force_com_dev_beginner)

You can get to Setup from any page in your Salesforce org. From the gear menu at the top of the screen ( ![Setup.](assets/d93a5f7ff918ea4432fe8e82dd562ee2_kix.t14uhi7bi2ft.jpeg)), click **Setup**.

<img src="assets/image-20250314202204041.png" alt="image-20250314202204041" style="zoom:50%;" />

- **Object Manager:** Object Manager is where you can view and customize standard and custom objects in your org.
- **Setup Menu:** The menu gives you quick links to a collection of pages that let you do everything from managing your users to modifying security settings.
- **Main Window:** We’re showing you the Setup home page, but this is where you can see whatever it is you’re trying to work on.

# CI

- CI in Salesforce Document: [Continuous Integration](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_ci.htm?_ga=2.255431115.2113438160.1742049829-1363362869.1742049829)
- Sample in Trailhead: [GitHub Actions](https://trailhead.salesforce.com/content/learn/projects/quick-start-tour-the-sample-app-gallery/learn-about-sample-app-tooling?trail_id=force_com_dev_beginner)

# Flows

**Flows** is a tool without codes.

More about Flows to learn: [Build Flows with Flow Builder](https://trailhead.salesforce.com/content/learn/trails/build-flows-with-flow-builder)

## Flows Basics

### Get to Flow Builder

- From **Setup**, select **Flows** in the **Quick Find** box.
- Click **New Flow**.
- Select **Start from Scratch** and click **Next**.
- Select **Screen Flow** and click **Create**.

### Interface

<img src="assets/image-20250311220230555.png" alt="image-20250311220230555" style="zoom:50%;" />

- **Toolbox (1)** : The toolbox lists the elements and resources you’ve built in your flow.
- **Canvas (2)** : The canvas is the working area.
- **Button Bar (3)**: Provide some tools.
    - More refer to: [Button Bar](https://trailhead.salesforce.com/content/learn/modules/flow-basics/meet-flow-builder?trail_id=force_com_dev_beginner#button-bar-3)

### Building Blocks

- Flows use three building blocks: elements, connectors, and resources.

    <img src="assets/image-20250311221030163.png" alt="image-20250311221030163" style="zoom:50%;" />

### Elements

- **Elements** are nodes on the canvas that make things happen. To add an element to the canvas, click ![Add element](assets/13f5207391f198a601856fce8a8a6280_kix.10ac7o3ovpkx.jpeg).
- There're three types of elements.
    - Interaction
    - Data
    - Logic

### Connectors

- **Connectors** are lines on the canvas that define the path the flow takes when it runs.

### Resources

- **Resources** are containers that don’t appear on the canvas, but are referenced by the flow’s elements. Each resource contains a value or a formula that resolves to a value.

## Build a flow with Flow Builder

- Sample in Trailhead: [Low-code Tools & Automation](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/develop-without-code-01?trail_id=force_com_dev_beginner).
- From **Setup**, select **Flows** in the **Quick Find**.
- Click the **Create Property** flow.
- Click ![Toolbox](assets/fa9fe34c482cca646a9b444e500a4d3c_kix.9by05x8kzn4r.jpg) to open the Toolbox menu.
- Click ![Resize and center](assets/bb02275e478118bc1f4ee474fb2b24e2_kix.jrjheih9gfgy.jpg) to resize the flow so you can see it all.
- Click **Run**. A **Create Property** form appears to collect details for a new property record.
- Fill out any details you like. Click **Next**, **Next**, and **Finish**.
- Click ![Exit](assets/4b049ec5ccc16bf4d97052b60f31f63f_kix.w2qp1uytpfbx.jpg) to exit Flow Builder.
- Select **Dreamhouse** from **App Launcher**.
- Click the **Properties** tab.
- Click the property you just created in Flow Builder.

## [Variables](https://trailhead.salesforce.com/content/learn/modules/flow-basics/learn-about-flow-variables)

-  A **variable** is a container that holds a piece of information. It's a kind of **Resources**.

- Variable types:
    - **Text**: A string of letters, numbers, and characters.
    - **Number, Currency:** A numerical value.
    - **Boolean**: A true or false value.
    - **Date, Date/Time**: A specially formatted value that indicates a specific date, or a specific time on a specific date. 
    - **Record**: All of the values in a Salesforce record, stored together in a single variable.
    - ...


### Create a Variable

- Sample in Trailhead: [Learn About Flow Variables](https://trailhead.salesforce.com/content/learn/modules/flow-basics/learn-about-flow-variables?trail_id=force_com_dev_beginner)
- From **Setup**, select **Flows** in the **Quick Find** box.
- Click **New Flow**.
- Select **Start from Scratch** and click **Next**.
- Select **Screen Flow** and click **Create**.
- Click ![Toggle Toolbox](assets/1121645553b3bb884e333a7e2271ec97_kix.im3gqi7i1ify.jpeg) to display the **Toolbox**.
- Click **New Resource**. 
- For **Resource Type**, select **Variable**.
- For **API Name**, enter `contactID`.
- For **Description**, enter `The Salesforce ID of the primary contact.`
- For **Data Type**, select **Text**.
- Click **Done**.
- Check the new variable in the **Toolbox**.

## [Constants](https://trailhead.salesforce.com/content/learn/modules/flow-basics/learn-about-flow-variables)

- **Constant** is a kind of **Resources**.

# [Formulas and Validation](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic?trail_id=force_com_dev_beginner)

## [Formulas](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/formula_fields?trail_id=force_com_dev_beginner)

### Code Formatting

- Case sensitive.
- Whitespace and line breaks don’t matter.

### Formula Basics

**Find the Formula Editor:**

- Sample in Trailhead: [Find the Formula Editor](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/formula_fields?trail_id=force_com_dev_beginner#find-the-formula-editor)
- **Setup** > **Object Manager** > **Opportunity** > **Fields & Relationships** > **New**
- For **Data Tyjpe**, select **Formula** and click **Next**.
- For **Field Label**, type `My Formula Field`.
- For **Formula Return Type**, select the type of data you expect your formula to return. For example, **Text**.
- Click **Next**. You’ve arrived at the **Formula Editor**.

**Use the Formula Editor:**

- Sample in Trailhead: [Use the Formula Editor](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/formula_fields?trail_id=force_com_dev_beginner#use-the-formula-editor)

    <img src="assets/image-20250321055847682.png" alt="image-20250321055847682" style="zoom: 67%;" />

- (1) The formula editor comes in two flavors: **Simple** and **Advanced**. There're more tools in **Advance**.

- (2) **Insert Field** button opens a dropdown list that allows you to select fields to use in your formula.

- (3) **Insert Operator** button opens a dropdown list of the available mathematical and logical operators.

- (4) **Functions** menu is where you insert formula functions.

- (5) Formula area.

- (6) Check your formula before saving.

### Creat Formulas

#### Sample 1

- Sample in Trailhead: [Example 1: Display an Account Field on the Contact Detail Page](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/formula_fields?trail_id=force_com_dev_beginner#example-1-display-an-account-field-on-the-contact-detail-page)

- Based on a new TP: **Use Formula Fields - learning**

- Create a new **Contact** record.

    - Select  **Contacts** from **App Launcher**.
    - For **Last Name**, enter any: **Bai**
    - For **Account Name**, enter an existing account such as `United Oil & Gas Corp`.
    - Click **Save**.

- Create a formula

    - **Setup** > **Object Manager** > **Contact** > **Fields & Relationships** > **New**
    - For **Data Tyjpe**, select **Formula** and click **Next**.
    - For **Field Label**, type `Account Number`.
    - For **Formula Return Type**, select **Text**.
    - Click **Next** to open the **Formula Editor**.
    - In the **Advanced Formula** editor, click **Insert Field**.
    - Select **Contact** | **Account** | **Account Number** and then click **Insert**.
    - Click **Check Syntax**. If there are no syntax errors, click **Next**, **Next**, and **Save**.

- Check the formular

    - Select **Contacts** from **App Launcher**.

    - Select the contact **Jerry Bai** from the contact list.

    - Click **Details** to check the formula **Account Number**.

        <img src="assets/image-20250321074106056.png" alt="image-20250321074106056" style="zoom:50%;" />

#### Sample 2

- Sample in Trailhead: [Example 2: Display the Number of Days Until an Opportunity Closes on a Report](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/formula_fields?trail_id=force_com_dev_beginner#example-2-display-the-number-of-days-until-an-opportunity-closes-on-a-report)
- Based on a new TP: **Use Formula Fields - learning**
- Creat a opptunity: **Opportunity-Jerry**
    - **App Launcher** > **Opportunities** > **New**
    - For **Opportunity Name**, enter any value: **Opportunity-Jerry**
    - For **Stage**, select any: **Prospecting**
    - For **Close Date**, at least 3 days.
    - Click **Save**.

- Creat a formula: **Days to Close**
    - **Setup** > **Object Manager** > **Opportunity** > **Fields & Relationships** > **New**
    - For **Data Tyjpe**, select **Formula**.
    - For **Field Label**, type `Days to Close`.
    - For **Formula Return Type**, select **Number**.
    - Click **Next** to open the **Formula Editor**.
    - Click **Insert Field** and select **Opportunity | Close Date** and click **Insert**.
    - Select **Subtract** from **Insert Operator**.
    - Select **TODAY** from **Functions** menu on the right side of the editor, then click **Insert Selected Function**. 
    - Click **Check Syntax**. If there are no syntax errors, click **Next**, **Next**, and **Save**.

- Edit your formula, then click the check button.
- **Put your new formula field in a report.** 
    - **App Launcher > Reports** > **New Report**
    - Select **Opportunities** from **Search Report Types...** and click **Start Report**. Your opportunity appears in the **Report Preview** panel.
    - Make sure **Update Preview Automatically** is enabled.
    - Select **Days to Close** from **Add column...** field on the left side of the page.
- Check the **Days to Close ** field: **App Launcher** > **Opportunities** > **Details**

## [Roll-Up Summary](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/roll_up_summary_fields?trail_id=force_com_dev_beginner)

**Formula** fields calculate values using fields within **a single record**.

**Roll-up Summary** fields calculate values from **a set of related records**.

Roll-up summary fields are based on the master side of a master-detail relationship. 

### Creating the Summary Field

- Sample in Trailhead: [Creating the Summary Field](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/roll_up_summary_fields?trail_id=force_com_dev_beginner#creating-the-summary-field)
- Based on the TP: **Use Formula Fields - learning**
- From Setup, open **Object Manager** and click **Account**.
- **Setup** > **Object Manager** > **Account** > **Fields & Relationships** > **New**
- For **Data Tyjpe**, select **Formula**.
- For **Field Label**, type `Sum of Opportunities`.
- For **Summarized Object**, select **Opportunities**.
- For **Select Roll-Up Type**, select **SUM** and for **Field to Aggregate** select **Amount**.
- Click **Next**, **Next**, and **Save**.

##  [Validation Rules](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/validation_rules?trail_id=force_com_dev_beginner)

Validation rules verify that data entered by users in records meets the standards you specify before they can save it. 

When the validation rule returns a value of "True", this confirms that the data entered by the user contains an invalid value. 

### Creat a Validation Rule

1. Sample in Trailhead: [Creatinging a Validation Rule](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic/validation_rules?trail_id=force_com_dev_beginner#creating-a-validation-rule)
2. Based on the TP: **Use Formula Fields - learning**
3. **Setup** > **Object Manager** > **Account**
4. In the left sidebar, click **Validation Rules**.
5. Click **New**.
6. Enter the following properties for your validation rule:
    1. Rule Name: `Account_Number_8_Characters`
    2. Error Condition Formula: `LEN( AccountNumber) <> 8`
7. Error Message: `Account number must be 8 characters long.`
8. To check your formula for errors, click **Check Syntax**.
9. Click **Save** to finish.
10. Check the **Account_Number_8_Characters** rule
    1. **App Launcher** > **Accounts** > **New**
    2. For **Account Name**, type a name without the lenth equaling 8.
    3. An error message appears: **Account number must be 8 characters long.**


# Metadata

Any configuration done in the admin UI can be retrieved as **XML** formatted data (also known as **metadata**) and checked into version control.

[Metadata API](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_intro.htm)

## Retrieve Metadata from Salesforce to the Local Project

- Sample in Trailhead: [Retrieve Metadata from Salesforce to the Local Project](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/create-a-data-model-using-clicks).
- Based on the project **Dreamhouse**: [Create a New Salesforce Project](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner).

### With VS Code

- In the Activity Bar of VS Code, click **Org Browser** <img src="assets/a8f26bcea3309c7490124fbbde76218e_kix.p03d27ihoxp4.jpg" alt="Org Browser." style="zoom: 50%;" />.

    <img src="assets/image-20250315185254353.png" alt="image-20250315185254353" style="zoom:50%;" />

- Locate **Custom Objects** > **House__c**.

- Click <img src="assets/cd2226227c13f749ce4defb219e7d4f3_kix.7smvyxr29llr.jpg" alt="Retrieve source from org." style="zoom:50%;" /> to retrieve the org metadata for the **House__c object**.

    <img src="assets/image-20250315185630681.png" alt="image-20250315185630681" style="zoom:50%;" />

- Notice that the XML files are under the **force-app/main/default/objects** folder.

    <img src="assets/image-20250315190408658.png" alt="image-20250315190408658" style="zoom:50%;" />

### With Salesforce CLI

- Execute the following command in the root directory of the project with **PowerShell**.

    ```bash
    sf project retrieve start --metadata CustomApplication:Dreamhouse CustomTab:House__c "Layout:House__c-House Layout"
    ```

# Lightning Apps

## [Lightning Apps Basics](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_apps?trail_id=force_com_dev_beginner)

An **app** is a collection of items that work together to serve a particular function. In Lightning Experience, **Lightning apps** give your users access to sets of objects, tabs, and other items all in one convenient bundle in the navigation bar.

![image-20250319063650568](assets/image-20250319063650568.png)

- The app name (1) displays on the left side of the navigation bar and custom colors.
- You can access other items and apps by clicking the **App Launcher** icon (3).

## Install an App

- Sample in Trailhead: [Install the Dreamhouse App](https://trailhead.salesforce.com/content/learn/modules/starting_force_com/starting_intro?trail_id=force_com_dev_beginner)
- Launch a Trailhead Playground.
- Locate to **Playground Starter** from **App Launcher**.
- Click the **Get Your Login Credentials** tab and reset your password.
- Click the **Install a Package** tab. 
- Paste `04tKY000000LOv6YAG` into the **Package ID** field and click **Install**.
- Select **Install for All Users**, then click **Install**.
- When it prompts you to Approve Third-party access, click **Yes** and click **Continue**. This provides updated information to the map in the Dreamhouse App.
- When the installation completes, click **Done**. It'll spend about 10 minutes.
- Locate to **Dreamhouse** from **App Launcher**.
- Click the **Settings** tab, then click the **Import Data** button. This populates the app with sample data, including properties, contacts, and brokers.

## Create an App

- Sample in Trailhead: [Create an App](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/create-a-data-model-using-clicks?trail_id=force_com_dev_beginner).
- Based on the project **Dreamhouse**: [Create a New Salesforce Project](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner).
- From **Setup**, select `App Manager` in the **Quick Find**.
- Click **New Lightning App**.
- In the **App Details & Branding** window, enter these details.
    - For App Name, type `Dreamhouse`.
    - For the Image, download [dreamhouse-logo.png](https://github.com/trailheadapps/dreamhouse-lwc/blob/main/dreamhouse-logo.png) as **dreamhouse-logo.png** and upload it.
    - Click **Next**.
- On the **App Options** screen, select **Standard navigation**, then click **Next**.
- On the **Utility Items** screen, click **Next**.
- On the **Navigation Items** screen, select **Home**, **Houses**, **Reports**, and **Dashboards** from the **Available Items** list, and move them to the **Selected Items** list using the arrow. Ensure you choose the pink **Home** tab. Then click **Next**.
- On the **User Profiles** screen, select **System Administrator**, add it to **Selected Profiles**, and then click **Save & Finish**.
- Select **Dreamhouse** from **App Launcher** to check the new App.

## Sample Apps

- Sample Apps in GitHub: https://github.com/trailheadapps

# Lightning Apps Builder

Maybe the sample is going to creat an app.

- Sample in Trailhead: [Lightning Apps Builder](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_apps?trail_id=force_com_dev_beginner)
- From **Setup**, select `Lightning App Builder` in the **Quick Find**.
- From the **Lightning Pages** list, select **Property Record Page**.
- Click **Edit**.
- Drag the any custom and drop them in the canvas in the center.

# [Lightning Experience Customization](https://trailhead.salesforce.com/content/learn/modules/lex_customization?trail_id=force_com_dev_beginner)

## Compact Layouts

- Sample in Trailhead: [Create a Compact Layout](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_compact_layouts?trail_id=force_com_dev_beginner)

## Page Laouts

**Setup** > **Object manager** > object > side bar > **Page Laouts**

There are two action sections on a page layout. The Quick Actions in the Salesforce Classic Publisher section controls which actions appear on record pages in the Salesforce Classic UI. The Salesforce Mobile and Lightning Experience Actions section controls which actions appear on record pages in both Lightning Experience and in the Salesforce mobile app. If you don’t customize the action sections of a page layout, then the actions you see in the Salesforce app and in Lightning Experience come from a set of default actions defined by Salesforce.

![image-20250321035135437](assets/image-20250321035135437.png)

## Component and Field

- When the **Energy Audit** custom object was created, a system default **Energy Audit** record page was created too. You can customiz it with **Lightning App Builder**.

- Samples in Trailhead: [Customize Record Page Components and Fields](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)
- Based on
    - TP: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
    - Sample: All above in Trailhead.

### Customiz Record Details

- Sample in Trailhead: [Create a Custom Lightning Record Page](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)
- From **App Launcher**, select the **Energy Consultations** app, then click the **Energy Audits** tab.
- Open the **All** list view.
- Select any record, for example **Burlington evaluation**.
- From **Setup**, select **Edit Page**. The page will open in the **Lightning App Builder**.
- In the **Page** properties on the rihgt:
    - Change the **Label** to `Energy Audit Record Page for Sales`.
    - Change the **API Name** to `Energy_Audit_Record_Page_for_Sales`.
    - Click the **Details** tab on the canvas, then click the **Record Detail** component (where the fields are).
    - In the properties pane, click **Upgrade Now** to start the **Dynamic Forms** migration wizard.
- In the **Dynamic Forms** properties:
    - Step through the wizard, select **Energy Audit Layout**, then click **Finish**.
    - Drag the **Audit Notes** field to the right column, above **Owner**.
    - Drag the **Type of Installation** field above **Audit Notes**.
    - Click **Save**, then **Not Yet**. 
    - Activating the page makes it available to your users. However, this page isn’t quite ready for users. Maria wants to add a related list.
- Click **Back** <img src="assets/0ede54fde552b239f646b0947605d914_i.40.jpg" alt="Back" style="zoom: 50%;" /> in the App Builder header.

### Customiz Record Lists

- Sample in Trailhead: [Customize Related Lists](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)

- Based on the sample: [Create a Custom Lightning Record Page](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)

- **Setup** > **Object Manager**

- Select the **Energy Audit** object.

- Click **Page Layouts** in the side bar, then **Energy Audit Layout**.

- Scroll down to the **Related Lists** section.

- In the palette, click **Related Lists**, and drag the **Files** element down to the **Related Lists** section. With the Files related list, Ursa Major Solar sales reps can add files to a record and see a list of files associated with the record.

    <img src="assets/image-20250320030637411.png" alt="image-20250320030637411" style="zoom:50%;" />

- Click **Quick Save**, then click **Yes**.

### Activate the Page

- Sample in Trailhead: [Activate the Page](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)
- Based on the sample: [Customize Related Lists](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)
- From **Setup**, select **Lightning App Builder**.
- Click **Edit** next to the **Energy Audit Record Page for Sales**.
- Click **Activation** icon in the top righy corner.
    - More activation options refer to: [Activate the Page](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)
- Click the **App, Record Type, and Profile** tab.
- Click **Assign to Apps, Record Types, and Profiles**.
- Step through the wizard, and select: **Energy Consultations** > **Desktop and phone** > **Master** > **Custom: Sales Profile** and **System Administrator**.
    - Normally, select only **Custom: Sales Profile**, but since you’re logged in as a System Administrator, we select **System Administrator** too so that you can see how the new page layout looks.
- Review the page assignments. Then click **Save**.

### View the Customized Page

- Sample in Trailhead: [View the Customized Page](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)

- Based on the sample: [Activate the Page](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_page_layouts?trail_id=force_com_dev_beginner)

- Click **Back** <img src="assets/0ede54fde552b239f646b0947605d914_i.43.jpg" alt="Back" style="zoom:50%;" /> in the App Builder header.

- From **App Launcher**, select **Energy Audits**.

- Open any record, for example **Burlington evaluation**. The **Details** and **Related** have been changed.

- **Details**

    <img src="assets/image-20250320035929784.png" alt="image-20250320035929784" style="zoom: 50%;" />

- **Related**

    <img src="assets/image-20250320040021483.png" alt="image-20250320040021483" style="zoom:50%;" />

    

## Button and Link

- Samples in Trailhead: [Create Custom Buttons and Links](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_buttons_links?trail_id=force_com_dev_beginner)
- Based on
    - TP: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
    - Sample: All above in Trailhead.

### Create a Custom List Button

- Samples in Trailhead: [Create a Custom List Button](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_buttons_links?trail_id=force_com_dev_beginner)

- From the **App Launcher**, select the **Sales** app.

- Click the **Files** tab. Here, Maria can see the guidelines PDF she uploaded.

- Upload a new PDF file of your own so you can follow along with the rest of these steps.

- Click ![Action dropdown](assets/03ba3588c34c126bfc752714a836a39f_i.48.png) for the file you just uploaded and select **Share**.

- Click **Who Can Access** to expand that section.

    - In the **Create Public Link** area, set the **Password** button to **Off**.
    - Click **Create Link**, then click **Create**. This generates a public URL for the file that you can share with others, or in this case, add as a URL to a custom button or link.
    - Click **Copy Link**, then click **Done**.

- From **Setup**, click **Object Manager**, then select the **Energy Audit** object.

- Select **Buttons, Links, and Actions** in the side bar, then **New Button or Link**.

- Name the button `Audit Guidelines`.

- Select **List Button**.

- Paste the file URL into the large text box.

    - Because the file is local to your org, use everything after the domain portion of the URL to create the custom link.

        <img src="assets/image-20250320052545576.png" alt="image-20250320052545576" style="zoom:50%;" />

- Click **Save**, then **OK**.

- Click **Object Manager**, then click **Account**.

- Click **Page Layouts**, then click **Account Layout**.

- Scroll all the way down the end of the layout, to the **Energy Audits** related list.

- Click the wrench icon (<img src="assets/01A47D43.png" alt="01A47D43" style="zoom:50%;" />) to edit it. 

- Click the plus icon (+) to expand the **Buttons** section header. 

- Add the **Audit Guidelines** button to the **Selected Buttons** list, then click **OK**.

- Click **Save**.

- From **App Launcher** select the **Sales** app.

- Click **Accounts** tab and select the **GenePoint** account.

- Click the **Related** tab, scroll to the bottom, and you see the new **Audit Guidelines** button on the **Energy Audits** related list. 

    ![image-20250320054452296](assets/image-20250320054452296.png)

### Create a Custom Detail Page Link

- Samples in Trailhead: [Create a Custom Detail Page Link](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_buttons_links?trail_id=force_com_dev_beginner)

- From **Setup**, click **Object Manager**, then select the **Account** object.

- Select **Buttons, Links, and Actions** in the side bar, then **New Button or Link**.

- Name the link `Google This Account`.

- For **Display Type**, select **Detail Page Link**.

- In the formula editor, enter `https://www.google.com/search?q={!Account.Name}`.

- Click **Save**, then click **OK**.

- Add the link to **Account** page layout.

    - From the **Account** object, click **Page Layouts** in the side bar, then **Account Layout**.

    - From the **Custom Links** category in the palette, drag **Google This Account** into the **Custom Links** section of the layout.

        <img src="assets/image-20250321002955639.png" alt="image-20250321002955639" style="zoom:50%;" />

    - Hover over the **Custom Links** section and click the wrench icon (<img src="assets/002E4FE5.png" alt="002E4FE5" style="zoom:50%;" />) that appears on the right of the screen.

    - In the **Section Properties** window, select **Detail Page**, then click **OK**.

- Check the link

    - From **App Launcher**, select **Accounts**.
    - Open an account record.
    - Click the **Details** tab and scroll to the bottom to find the **Custom Link**.


### Create a Custom Detail Page Button

- Samples in Trailhead: [Create a Custom Detail Page Button](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_buttons_links?trail_id=force_com_dev_beginner)

- From **Setup**, click **Object Manager**, then select the **Account** object.

- Select **Buttons, Links, and Actions** in the side bar, then **New Button or Link**.

- Name the button `Map Location`.

- For **Display Type**, select **Detail Page Button**.

- In the formula editor, enter `http://maps.google.com/maps?q={!Account_BillingStreet}%20{!Account_BillingCity}%20{!Account_BillingState}%20{!Account_BillingPostalCode} `

- Click **Save**, then click **OK**.

- Add the button to **Account** page layout.

    - From the **Account** object, click **Page Layouts** in the side bar, then **Account Layout**.

    - From the **Buttons** category in the palette, drag **Map Location** into the **Custom Buttons** section of the layout.

        ![image-20250321005751460](assets/image-20250321005751460.png)

- Check the button

    - From **App Launcher**, select **Accounts**.

    - Open an account record.

        ![image-20250321011906704](assets/image-20250321011906704.png)

## Action

Action is a kind of shortcuts.

### Create an Object-Specific Action

**Create an Object-Specific Action:**

- Sample in Trailhead: [Create an Object-Specific Action](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_actions?trail_id=force_com_dev_beginner#create-an-object-specific-action)
- From **Setup**, click **Object Manager**, then select the **Account** object.
- Select **Buttons, Links, and Actions** in the side bar, then **New Action**.
- For **Action Type**, select **Create a Record**.
- For **Target Object**, select **Energy Audit**.
- For **Label**, enter `New Energy Audit`.
- Click **Save**.

**Add an Object-Specific Action to a Page Layout:**

- Sample in Trailhead: [Add an Object-Specific Action to a Page Layout](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_actions?trail_id=force_com_dev_beginner#add-an-object-specific-action-to-a-page-layout)

- From the **Account** object, click **Page Layouts** in the side bar, then **Account Layout**.

- In the **Salesforce Mobile and Lightning Experience Actions** section, click ![override global publisher layout](assets/14c540eae50648ed30fab2df74caa6d2_i.61.png) to override the defaults.

- Then you'll see a combination of the default actions and custom and standard buttons on the page layout.

- Select **Mobile & Lightning Actions** in the palette and then drag the **New Energy Audit** action to the **Salesforce Mobile and Lightning Experience Actions** section.

    ![image-20250321040427699](assets/image-20250321040427699.png)

- You can adjust the order of the actions by dragging them around.

- Click **Save**.

Check the **New Energy Audit** action

![image-20250321042358442](assets/image-20250321042358442.png)

### Create a Global Action

**Create a Global Action:**

- Sample in Trailhead: [Create a Global Action](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_actions?trail_id=force_com_dev_beginner#create-a-global-action)

- From **Setup**, click the **Home** tab.

- Select **Global Actions** from **Quick Find** box.

- Click **New Action**.

- For **Action Type**, select **Create a Record**.

- For **Target Object**, select **Campaign**.

- For **Label**, enter `New Campaign`.

- Click **Save**.

- On the action layout, remove the **Parent Campaign** field and add the **Expected Revenue in Campaign** and **Campaign Owner** fields.

    ![image-20250321044043109](assets/image-20250321044043109.png)

- Click **Save**.

**Add a Global Action to the Global Actions Menu:**

- Sample in Trailhead: [Add an Object-Specific Action to a Page Layout](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_actions?trail_id=force_com_dev_beginner#add-a-global-action-to-the-global-actions-menu)

- From the **Account** object, click **Page Layouts** in the side bar, then **Account Layout**.

- From **Setup**, click the **Home** tab.

- Select **Publisher Layouts** from **Quick Find** box.

- Click **Edit** next to **Global Layout**.

- In the **Salesforce Mobile and Lightning Experience Actions** section, click ![override global publisher layout](assets/14c540eae50648ed30fab2df74caa6d2_i.67.png) to override the defaults.

- Click the **Mobile & Lightning Actions** category in the palette.

- Drag **New Campaign** from the palette into the **Salesforce Mobile and Lightning Experience Actions** section.

    ![image-20250321045200333](assets/image-20250321045200333.png)

- Click **Save**.

- Check the **New Campaign** action

    ![image-20250321045414480](assets/image-20250321045414480.png)

# [Lightning Web Components](https://trailhead.salesforce.com/content/learn/modules/lightning-web-components-basics)

**Lightning web components (LWC)** are custom HTML elements that use the [Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) standards and are built with HTML and JavaScript. A LWC runs in the browser natively and allows developers to customize the out-of-the-box user interface.

## Build a Reusable UI Component with Lightning Web Components

- Sample in Trailhead: [Build a Reusable UI Component with Lightning Web Components](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/build-reusable-ui-component-with-lightning-web-components?trail_id=force_com_dev_beginner).
- Based on the project **Dreamhouse**: [Create a New Salesforce Project](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner).

### Create and Deploy a Lightning Web Component

- Under the **force-app/main/default** folder, right-click the **lwc** folder and select **SFDX: Create Lightning Web Component**.

- Name the Lightning web component `housingMap` and select the **main/default/lwc** directory.

- You see these files: an HTML file, a JavaScript file, a metadata XML file, and a test.js file.

    ![image-20250317022341519](assets/image-20250317022341519.png)

- In the HTML file, **housingMap.html**, copy and paste the following code.

    ```html
    <template>
      <lightning-card title="Housing Map">
        <!-- Explore all the base components via Base component library
        (https://developer.salesforce.com/docs/component-library/overview/components)-->
          <lightning-map map-markers={mapMarkers}> </lightning-map>
      </lightning-card>
    </template>
    ```

- In the JavaScript file, **housingMap.js**, copy and paste the following code.

    ```javascript
    import { LightningElement, wire } from "lwc";
    import getHouses from "@salesforce/apex/HouseService.getRecords";
    export default class HousingMap extends LightningElement {
        mapMarkers;
        error;
        @wire(getHouses)
        wiredHouses({ error, data }) {
            if (data) {
            console.log(data);
        }
      }
    }
    ```

    **Notice**: The Lightning web component invokes the Apex class **HouseService** you wrote in the previous section to fetch the data.

- Next, let's add code to transform the data as needed by the [lightning-map](https://developer.salesforce.com/docs/component-library/bundle/lightning-map/documentation) Base component. Replace the code with the following lines.

    ```javascript
    import { LightningElement, wire } from "lwc";
    import getHouses from "@salesforce/apex/HouseService.getRecords";
    export default class HousingMap extends LightningElement {
        mapMarkers;
        error;
        @wire(getHouses)
        wiredHouses({ error, data }) {
            if (data) {
             // Use JavaScript Map function to transform the Apex method response wired to the component into the format required by lightning-map
              this.mapMarkers = data.map((element) => {
                    return {
                        location: {
                            Street: element.Address__c,
                            City: element.City__c,
                            State: element.State__c
                        },
                        title: element.Name
                    };
                });
                this.error = undefined;
            } else if (error) {
                this.error = error;
                this.mapMarkers = undefined;
            }
        }
    }
    ```

- In the XML file, **housingMap.js-meta.xml**, Replace the code with the following lines.

    ```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata">
        <apiVersion>63.0</apiVersion>
        <isExposed>true</isExposed>
        <targets>
          <target>lightning__HomePage</target>
        </targets>
    </LightningComponentBundle>
    ```

- Right click and select **SFDX: Deploy This Source to Org**.

### Add the Component to the App Home

- Select **Dreamhouse** from **App Launcher**.

- Click **Home** tab in the top navigation menu.

- Select **Edit Page** from **Setup**.

- Drag the **housingMap** Lightning web component from the **Custom** area of the Lightning Components list to the top of the **Page Canvas**.

    ![image-20250317025743959](assets/image-20250317025743959.png)

- Click **Save** > **Activate** > **Assign as Org Default** > **Save** > **Save**.

- Click <img src="assets/75efa403f72272b560fc21f87d2ec625_kix.bnc114cd4e6.jpg" alt="Back" style="zoom: 33%;" /> to return to the page.

- Refresh the page to view your new component.

    <img src="assets/image-20250317030231300.png" alt="image-20250317030231300" style="zoom: 33%;" />

# [List Views](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_list?trail_id=force_com_dev_beginner)

## Create a List View

- Sample in Trailhead: [Create a List View](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_list?trail_id=force_com_dev_beginner)

- Based on:

    - TP: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
    - Sample: [Create a Lightning App](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_apps?trail_id=force_com_dev_beginner)

- **App Launcher** > **Sales** > **Accounts** > **New**

    ![image-20250305183252478](assets/image-20250305183252478.png)

- Name the list `Channel Customers`.

- Select **All users can see this list view**.

- Click **Save**.

- **Add Filter**

    - Click **Add Filter**.
    - From the **Field** dropdown menu, select **Type**.
    - Select the **equals** operator.
    - For Value, select **Customer - Channel**, then click **Done** and **Save**.
    - Add another filter where **Billing State/Province** equals **WA,OR,CA**.

- Customize a List View

    - From the list view controls <img src="assets/0ce868631cd88aaf9e2ddfdac636fcee_i.20.png" alt="List View Controls" style="zoom: 25%;" />, you can custom your list view again.


## Create a List View Chart

- Sample in Trailhead: [Create a List View Chart](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_list?trail_id=force_com_dev_beginner)

- Based on:
    - TP: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
    - Sample: [Create a List View](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_list?trail_id=force_com_dev_beginner)
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

# Package

## [Install a Package](https://trailhead.salesforce.com/help?article=Installing-a-package-or-app-to-complete-a-Trailhead-challenge)

# Project

## Create a Project

- Sample in Trailhead: [Create a New Salesforce Project](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner)

- **Precondition**

    - Create a new TP.

    - Install Salesforce CLI.

    - Install VS Code and the Salesforce Extension Pack.

    - Install Node.js.

- **Create a Project**

    - Press **Ctrl+Shift+P** in VS Code to open the command palette, and type `SFDX`.
    - Select **SFDX: Create Project**.
    - Select **Standard**.
    - Type the project name and press **Enter**.
    - Set the project location.

- **Authorize**

    - Press **Ctrl+Shift+P** in VS Code to open the command palette, and type `SFDX: Authorize an Org`.
    - Select **Production** and type the organization alias `myDevOrg`. Then press **Enter**.
    - A webpage will pop up for login.
    - **Notice**: Type the username and password of your **org**.

- Ways to open an org.

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

- Reload VS Code.

## Project Configurations

- Sample in Trailhead: [Salesforce Project Configurations](https://trailhead.salesforce.com/content/learn/projects/quick-start-tour-the-sample-app-gallery/learn-about-sample-app-tooling?trail_id=force_com_dev_beginner)

- Based on the project on GitHub: [lwc-recipes](https://github.com/trailheadapps/lwc-recipes)

- Get to know the Salesforce project setup in the `sfdx-project.json` config file.

- **sfdx-project.json**

    ```json
    {
      "packageDirectories": [
        {
          "path": "force-app",
          "default": true,
          "package": "LWCRecipes",
          "versionName": "Spring '24",
          "versionNumber": "62.0.0.NEXT"
        }
      ],
      "namespace": "",
      "sourceApiVersion": "62.0",
      "sfdcLoginUrl": "https://login.salesforce.com",
      "packageAliases": {
        "LWCRecipes": "0Ho3t000000KywNCAS",
        "LWCRecipes@59.0.0-20": "04t3t000002YSCcAAO",
        "LWCRecipes@60.0.0-1": "04t3t000002YSCrAAO",
        "LWCRecipes@60.0.0-4": "04t3t000002lhjcAAA",
        "LWCRecipes@60.0.0-7": "04t3t000002lhk1AAA",
        "LWCRecipes@60.0.0-9": "04t3t000002lhkaAAA",
        "LWCRecipes@60.0.0-10": "04t3t000002lhkfAAA",
        "LWCRecipes@60.0.0-12": "04t3t000002lhkpAAA",
        "LWCRecipes@61.0.0-1": "04t3t000002lhpRAAQ",
        "LWCRecipes@61.0.0-6": "04t3t000002lhucAAA",
        "LWCRecipes@61.0.0-7": "04t3t000002lhvLAAQ",
        "LWCRecipes@61.0.0-11": "04t3t000002li3GAAQ",
        "LWCRecipes@61.0.0-13": "04t3t000002li3QAAQ",
        "LWCRecipes@62.0.0-1": "04t3t000002li7xAAA"
      }
    }
    ```

- More explanations in Trailhead: [Salesforce Project Configurations](https://trailhead.salesforce.com/content/learn/projects/quick-start-tour-the-sample-app-gallery/learn-about-sample-app-tooling?trail_id=force_com_dev_beginner)

## npm

- Even though most projects don’t use Node.js in any runtime Salesforce code, we still have a `package.json` to import and configure the developer tools with npm.  
- Sample in Trailhead: [Code Quality Tool Setup](https://trailhead.salesforce.com/content/learn/projects/quick-start-tour-the-sample-app-gallery/learn-about-sample-app-tooling?trail_id=force_com_dev_beginner)
- Based on the project on GitHub: [lwc-recipes](https://github.com/trailheadapps/lwc-recipes)

# Schema Builder

## Visualize data model with Schema Builder

- Sample in Trailhead: [See Your Data Model in Action](https://trailhead.salesforce.com/content/learn/modules/data_modeling/schema_builder?trail_id=force_com_dev_beginner)
- Based on TP: [Optimize Customer Data with Standard and Custom Objects](https://trailhead.salesforce.com/content/learn/modules/data_modeling/objects_intro?trail_id=force_com_dev_beginner)
    - Custom Object: **Property**
    - Custom Object **Favorite**: [Create a Custom Object](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)
    - Challenge
        - Custom Object: **Offer**
- From **Setup**, select **Schema Builder** in the **Quick Find** box. 
- In the left panel, click **Clear All**.
- Check **Contact**, **Favorite**, **Offer**, and **Property**.
- Click **Auto-Layout**.

## Create an Object with Schema Builder

- Sample in Trailhead: [Create an Object with Schema Builder](https://trailhead.salesforce.com/content/learn/modules/data_modeling/schema_builder?trail_id=force_com_dev_beginner)
- From **Setup**, select **Schema Builder** in the **Quick Find** box. 
- In the left sidebar, click the **Elements** tab.
- Click **Object** and drag it onto the canvas.
- Enter information about your object. You can make it whatever you want! **Object - Schema Builder**
- Click **Save**.
- Check the new object **Object - Schema Builder** as usual.

## Create a Field with Schema Builder

- Sample in Trailhead: [Create a Field with Schema Builder](https://trailhead.salesforce.com/content/learn/modules/data_modeling/schema_builder?trail_id=force_com_dev_beginner)
- From **Setup**, select **Schema Builder** in the **Quick Find** box. 
- In the left sidebar, click the **Elements** tab.
- From the **Elements** tab, choose a field type and drag it onto the object you just created.
- Fill out the details about your new field. **Email - Schema Builder**
- Click **Save**.
- Check the new field **Email - Schema Builder** as usual.

# Solution

| Solution            | Form | Conditional logic and actions | Requires Code |
| :------------------ | :--- | :---------------------------- | :------------ |
| Quick action        | Yes  | No                            | No            |
| Flow                | Yes  | Yes                           | No            |
| Lightning component | Yes  | Yes                           | Yes           |

# Tab

## Create a Custom Object Tab

- Sample in Trailhead: [Create a Custom Object Tab](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_custom_objects?trail_id=force_com_dev_beginner)
- Based on the sample: [Create a Custom Object](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_custom_objects?trail_id=force_com_dev_beginner)
- For **Tab Style**, select the **Sun** color scheme and icon.
- For **Description**, type `Tab for the Energy Audit object.`.
- Click **Next**, then **Next** again.
- For the **Add to Custom Apps** screen, deselect **Include Tab**, and select only **Sales (standard__LightningSales)**. This is to make the tab visible for just the Sales users.
- Click **Save**.
