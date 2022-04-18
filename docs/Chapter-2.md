---
title: Getting Started  
excerpt: ""  
category: 6215975992e4610014e7b757
---



<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)

## Integration Steps
Its easy to get started with the Smile API! Implementing the Smile API involves simple client and server-side integration, which are outlined below in four key steps:

1. **Link token:** Your application server sends a request to our REST API to generate a short-lived "Link" token.

2. **Wink Widget:** Using the Link token, your application client initializes the client SDK to launch the Smile "Wink" widget. Your end-users interact with this widget to submit their login credentials to authenticate with their employment data provider over a secure and encrypted connection.

3. **Connecting to Source Data:** Once in the widget, a user can then either connect their employment account or upload a photo or scanned copy of their employment data. This will be used as the source for any user data your application will be requesting.

4. **Requests:** Our servers execute your application's requests. We read, transform, and temporarily store data from the user's employment data provider so that it can be sent to the client application.

<!--
5. **Webhooks (coming soon):** Webhooks can also be delivered to your server in cases where data will be processed asynchrounously. Messages via webhook will be sent whenever data becomes available or is updated. Your server can then fetch the data from our REST API.
-->

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## Using the Developer Portal
To get started, simply register to the [developer portal](https://portal.getsmileapi.com).

After registration, you will be given an API key and an API secret. The API secret must be kept safe and used only in exchanges between your application's server and Smile API's server.

---
<!-- focus: false -->
![Quickstart](https://img.icons8.com/ios/50/000000/speed.png)

## Quickstart 
> 📘 Note
> 
> We provide [Quickstart sample code](https://github.com/SmileAPI/quickstart) in [Github](https://github.com/SmileAPI) which you can download and modify according to your own requirements. 

The example code installs a small server running on Node.js that automatically retrieves a token from our API, so you can instantiate the Wink widget in your own local machine.

The example implementation is composed of two parts:
* Under /frontend, you will find example code in HTML that already has the Wink Javascript SDK embedded already.
* Under /node, you will find server-side Javascript code that will retrieve the token. You will need to download and run Node.js to run the code.

**Implementation Steps**

Below steps are also included in the README.md document included in the the Quickstart [repository](https://github.com/SmileAPI/quickstart).
1. Download the Quickstart files onto your machine. 

> 📘 Note
>
> If you have git, you can clone the repository or run the following command:

```bash
git clone https://github.com/SmileAPI/quickstart
```

2. Go to /node directory of Quickstart.

3. Create a new file with called ".env" in that directory.

4. Make sure you have proper permissions in your machine to be able to create the file. 

> 📘 Note
>  
> For example, in Mac or Linux machines open up the Terminal, you can use vi and enter the following commands as a Super User:

```bash
sudo touch .env
```

> 🚧 Warning
>  
> On Windows machines, Windows will not allow you to create a .env file directly from Windows Explorer since it will not allow file names starting with a ".". To get around this:

```bash
1. Open Notepad oand write the content of the file (see below).
2. Goto FILE-> SAVE AS Save as Screen in the notepad.
3. Select the All files() type in the selection window.
4. Save the file as ".env" 
```

5. Open up the ".env" file that you just created in your favorite editor, and enter the following:

```bash
# The port you want the example server to listen to
APP_PORT=<portnumber>

# Smile Link API keys (you can get this by requesting access from access@getsmileapi.com)
API_KEY_ID=<apikeyid>
API_KEY_SECRET=<apisecret>

# API Host (whether this will run in Sandbox or Production)
API_HOST=<apiURL>
```

> 🚧 Warning
> 
> The .env file is normally hidden by your system.** You may want to enable showing of hidden files in your system preferences to be able to see it. **You can use ".env.example" file, included in the Quickstart repository, as a reference.**


6. Save and close your file.

7. If you don't have Node.js installed in your machine, install Node.js. 

> 📘 Note
>
> For example on the Mac you can open up the Terminal and run:

```bash
curl "https://nodejs.org/dist/latest/node-${VERSION:-$(wget -qO- https://nodejs.org/dist/latest/ | sed -nE 's|.*>node-(.*)\.pkg</a>.*|\1|p')}.pkg" > "$HOME/Downloads/node-latest.pkg" && sudo installer -store -pkg "$HOME/Downloads/node-latest.pkg" -target "/"
```

> 📘 Note
>
> For Windows you can [download the installer](https://nodejs.org/en/#home-downloadhead).
> For other operating systems, [you can find the instructions](https://nodejs.org/en/download/package-manager/#macos) from the Node.js website.


8. Run Yarn with [npm package manager](https://www.npmjs.com/) which is included with Node.js and enter the following commands:

> 📘 Note
>
> In Mac or Linux, you will need to open up the Terminal. If you are using Windows, you can go to the command line. Make sure you are still in the /node directory of the Quickstart files you just downloaded onto your machine.

```bash
npm install --global yarn
yarn install
```

> 🚧 Warning
>
> You may need to run as a Super User if you don't have enough permissions. On a Mac or Linux machine, you can run the commands as a superuser by using 'sudo'. On Windows, you can run the command with an administrator trust-level, or by right-clicking the program in the UI and choosing "run as administrator."

8. Run the server:
```bash
node index.js
```

9. Open up the your browser and open up the example Wink Widget. For example, if you specified port:8000 in your ".env" configuration file, open up http://127.0.0.1:8000 in your web browser.

10. Test the Widget by using the [Sandbox accounts](ref:getting-user-data#testing-in-sandbox)

> 👍 Good job!
>
> Sit back, relax, and pat yourself on the back for a job well done!