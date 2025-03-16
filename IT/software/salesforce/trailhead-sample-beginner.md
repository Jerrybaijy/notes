# Salesforce Platform Basics

## [Install the Dreamhouse App](https://trailhead.salesforce.com/content/learn/modules/starting_force_com/starting_intro?trail_id=force_com_dev_beginner)

1. Launch a Trailhead Playground.
2. Locate to **Playground Starter** from **App Launcher**.
3. Click the **Get Your Login Credentials** tab and reset your password.
4. Click the **Install a Package** tab. 
5. Paste `04tKY000000LOv6YAG` into the **Package ID** field and click **Install**.
6. Select **Install for All Users**, then click **Install**.
7. When it prompts you to Approve Third-party access, click **Yes** and click **Continue**. This provides updated information to the map in the Dreamhouse App.
8. When the installation completes, click **Done**.
9. Locate to **Dreamhouse** from **App Launcher**.
10. Click the **Settings** tab, then click the **Import Data** button. This populates the app with sample data, including properties, contacts, and brokers.

## [Create a Field](https://trailhead.salesforce.com/content/learn/modules/starting_force_com/starting_intro?trail_id=force_com_dev_beginner)

- Install the APP **Dreamhouse**.
- From **Setup**, locate to **Object Manager** > **Contact**.
- In the sidebar, click **Fields & Relationships**. 
- Click **New** in the top right.
    - For **data type**, select **Checkbox** and click **Next**.
    - Type `Prequalified?` in the **Field Label** field, and **Field Name** field auto-fill.
    - Click **Next**, **Next** again to accept the default field-level security.
    - Check the checkboxes to add the new field to all the Contact Page Layouts.
    - Click **Save**.
- Check the new field:
    - Locate to **Dreamhouse** from **App Launcher**.
    - Click the **Contacts** tab, then click a contact name.
    - Under the **Details** tab, you can see your new field **Prequalified?**.

# Platform Development Basics

## [Install the Dreamhouse App](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/get-started-with-the-salesforce-platform-01?trail_id=force_com_dev_beginner)

- Install the Dreamhouse App again with the new Packge ID `04t3h000004bhxlAAA`.

## [Schema Builder](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/develop-without-code-01?trail_id=force_com_dev_beginner)

- Click **Setup**.
- Locate **Schema Builder** from **Quick Find** box.
- From the **Objects** tab, click **Clear All**.
- Select **Custom Objects** from the picklist.
- Select **Broker** and **Property** in the bottom left. Then you can see the legend.
- Click **Auto-Layout** to bring the **Broker** and **Property** custom object schemas into view.

## [Lightning Apps Builder](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_apps?trail_id=force_com_dev_beginner)

- Click **Setup**.
- Locate **Lightning App Builder** from **Quick Find** box.
- From the **Lightning Pages** list, select **Property Record Page**.
- Click **Edit**.
- ...........

## [Low-code Tools & Automation](https://trailhead.salesforce.com/content/learn/modules/lex_customization/lex_customization_apps?trail_id=force_com_dev_beginner)

- Introduce **Flows**.

## [Code with Salesforce Languages](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/code-with-salesforce-languages-01?trail_id=force_com_dev_beginner)

When developing with the Salesforce Platform there are a number of programming languages you can use, including: 

- **Lightning Web Component Framework**: A JavaScript-based User Interface (UI) development framework similar to AngularJS or React.
- **Apex**: Salesforce’s proprietary programming language with Java-like syntax.
- **Node.js**: An asynchronous, event-driven JavaScript runtime designed to build scalable network applications.

## [Extend the Salesforce Platform](https://trailhead.salesforce.com/content/learn/modules/platform-development-basics/extend-the-salesforce-platform-01?trail_id=force_com_dev_beginner)

Introduce how to Extend the Salesforce Platform:

- API
- Heroku
- Einstein

# Get Started with Salesforce Development

## [Get Ready to Develop](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner)

- Creat a new TP.
- Install Salesforce CLI.
- Install VS Code and the Salesforce Extension Pack.

### [Create a New Salesforce Project](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner)

- **Precondition**

    - Create a new TP.

    - Install Salesforce CLI.

    - Install VS Code and the Salesforce Extension Pack.

    - Install Node.js.

- **Create a Project**

    - Press **Ctrl+Shift+P** in VS Code to open the command palette, and type **SFDX**.
    - Select **SFDX: Create Project**.
    - Select **Standard**.
    - Type the project name and press **Enter**.
    - Set the project location.

- **Authorize**

    - Press **Ctrl+Shift+P** in VS Code to open the command palette, and type **SFDX: Authorize an Org**.
    - Select **Production** and type the organization alias **myDevOrg**. Then press **Enter**.
    - A webpage will pop up for login.
    - **Notice**: Type the username and password of your **org**.

- Ways to open an organization.

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

























1111

1111