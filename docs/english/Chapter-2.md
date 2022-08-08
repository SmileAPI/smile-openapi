---
title: Getting Started  
excerpt: ""  
category: 6215975992e4610014e7b757
slug: chapter-2
---



<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)

## Integration Steps
Its easy to get started with the Smile API! Implementing the Smile API involves simple client and server-side integration, which are outlined below in four key steps:

1. **Link token:** Your application server sends a request to our REST API to generate a short-lived "Link" token.

2. **Wink Widget:** Using the Link token, your application client initializes the Client SDK to launch the Smile Wink Widget. Your end-users interact with this widget to submit their login credentials to authenticate with their employment data provider over a secure and encrypted connection.

3. **Connecting to Source Data:** Once in the widget, a user can then either connect their employment account or upload a photo or scanned copy of their employment data. This will be used as the source for any user data your application will be requesting.

4. **Requests:** Our servers execute your application's requests. We read, transform, and temporarily store data from the user's employment data provider so that it can be sent to the client application.

<!--
5. **Webhooks (coming soon):** Webhooks can also be delivered to your server in cases where data will be processed asynchrounously. Messages via webhook will be sent whenever data becomes available or is updated. Your server can then fetch the data from our REST API.
-->

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## Using the Developer Portal
To get started, simply register to the [Developer Portal](https://portal.getsmileapi.com). After registering, you will be asked to verify your email and then you can log in. 

By default, when you register and log in, you will be in "Sandbox" mode. You can access "Production" mode by booking a call or emailing access@getsmileapi.com, and submitting the necessary information to go live. 

> 📘 Note
> 
> To learn more about the different modes, check out the next section on **"Understanding the API"**

Inside the Developer Portal, you will see the following:

1. **Wink Widget:** Use this to preview how the Wink Widget works. The behavior of the widget changes depending on the mode you are in. In Sandbox mode, you can use the provided test accounts on the page to simulate the process of logging into different data providers such as a gig platform or payroll system.  In Production mode, you will be able to actually link a live account or upload an actual file. 

2. **Users:** View the users created in the back-end, as well as the data captured from that user, during the account linking process or after uploading the user uploads a file. In this section, you can also preview how the returned data from Smile looks like for each resource such as Employments and Incomes.

3. **Data Source:** The Data Source section is where you can find all the Data providers as well as File Types that can be uploaded. Data providers include different types such as the names of different employers, gig platforms, government services, or HR and payroll systems. File types on the other hand are those that can be uploaded by the user such as copies of payslips, tax documents and others.

4. **API Keys:** After registration, you will be given a Sandbox API key and an API secret. The API secret must be kept safe and used only in exchanges between your application's server and Smile API's server. Upon request, you can also be given the API key and API secret to use the Smile API in production. This will also allow you to switch the Developer Portal to "Production Mode" for live testing.

5. **Organizations:** This is where you can enter details about your organization.

6. **Team:** This is where you can invite additional members from your organization to join the Portal and share a common tenant or workspace.

7. **Documentation:** This is a link to the API documentation which you are reading now!



---
<!-- focus: false -->
![Quickstart](https://img.icons8.com/ios/50/000000/speed.png)

## Quickstart 

To actually test the Smile API in your own environment, we have provided example code to instantiate the Wink Widget or SDK.

> 📘 Note
> 
> We provide [Quickstart sample code](https://github.com/SmileAPI/quickstart) in [Github](https://github.com/SmileAPI) which you can download and modify according to your own requirements. 

The example code installs a small server running on Node.js that automatically retrieves a token from our API, so you can instantiate the Wink widget in your own local machine.

The example implementation is composed of two parts:
* Under ``/frontend``, you will find example code in HTML that already has the Wink Javascript SDK embedded.
* Under ``/node``, you will find server-side Javascript code that will retrieve the token. You will need to download and run Node.js to run the code.

**Implementation Steps**

Below steps are also included in the README.md document found in the the Quickstart [repository](https://github.com/SmileAPI/quickstart).

1. **Download the Quickstart files onto your machine.**
   
   > 📘 Note
   >
   > If you have git, you can clone the repository or run the following command:
   > 
   > ```bash
   > git clone https://github.com/SmileAPI/quickstart
   > ```

2. **Go to the ``/node`` directory of your Quickstart download.**

3. **Create a new file called ``.env`` in this directory** with the following contents:
   
   ```bash
   # The port you want the example server to listen to
   APP_PORT=<portnumber>
   
   # Smile Link API keys (you can get this by requesting access from access@getsmileapi.com)
   API_KEY_ID=<apikeyid>
   API_KEY_SECRET=<apisecret>
   
   # API Host (whether this will run in Sandbox or Production)
   OPEN_API_HOST=<openapihost>
   # Link API Host
   LINK_API_HOST=<linkapihost>
   ```

   You can use the ``.env.example`` file, included in the Quickstart repository, as a reference.

   > 🚧 Warning
   > 
   > **The .env file is normally hidden by your system.** You may want to enable display of hidden files in your system preferences to be able to see it.
   >
   > Additionally, on Windows machines, Windows will not allow you to create a ``.env`` file directly from Windows Explorer since it will not allow file names starting with a ``.``. To get around this, you can do the following steps:
   > 
   > 1. Open Notepad and write the contents of the file (see below).
   > 2. Go to FILE -> SAVE AS window in Notepad.
   > 3. Select the "All files" type in the selection window.
   > 4. Save the file as ``.env``

   You may need to ensure that you have proper permissions in your machine to create the file.

   > 📘 Note
   >  
   > In Mac or Linux machines, you can open up Terminal and enter the following commands as a Super User:
   >
   > ```bash
   > sudo touch .env
   > ```
   
4. **Save and close your file.**

5. If you don't have Node.js installed in your machine, **install Node.js.**
   
   > 📘 Note
   >
   > **For Mac,** you can open up the Terminal and run:
   > ```bash
   > curl "https://nodejs.org/dist/latest/node-${VERSION:-$(wget -qO- https://nodejs.org/dist/latest/ | sed -nE 's|.*>node-(.*)\.pkg</a>.*|\1|p')}.pkg" > "$HOME/Downloads/node-latest.pkg" && sudo installer -store -pkg "$HOME/Downloads/node-latest.pkg" -target "/"
   > ```
   >
   > **For Windows,** you can [download the installer](https://nodejs.org/en/#home-downloadhead).
   >
   > **For other operating systems,** [you can find the instructions](https://nodejs.org/en/download/package-manager/#macos) from the Node.js website.

8. **Run Yarn** with [npm package manager](https://www.npmjs.com/) which is included with Node.js and enter the following commands:
   ```bash
   npm install --global yarn
   yarn install
   ```
   
   > 📘 Note
   >
   > In Mac or Linux, you will need to open up the Terminal. If you are using Windows, you can go to the command line. Make sure you are still in the ``/node`` directory of the Quickstart files you just downloaded onto your machine.
   > 
   > You may need to run as a Super User if you don't have enough permissions. On a Mac or Linux machine, you can run the commands as a superuser by using ``sudo``. On Windows, you can run the command with an administrator trust-level, or by right-clicking the program in the UI and choosing "run as administrator."

8. **Run the server:**
   ```bash
   node index.js
   ```

   > 🚧 Warning
   >
   > You may need to install dotenv in your environment if you run into issues running the Node server. To install dotenv, simply run the following:
   > 
   > ```bash
   > npm install dotenv
   > ```

9. **Open up the your browser and open up the example Wink Widget.** For example, if you specified port ``:8000`` in your ``.env`` configuration file, open up http://127.0.0.1:8000 in your web browser.

10. **Test the Widget** using the [Sandbox accounts](ref:getting-user-data#testing-in-sandbox) provided.

> 👍 Good job!
>
> Sit back, relax, and pat yourself on the back for a job well done!