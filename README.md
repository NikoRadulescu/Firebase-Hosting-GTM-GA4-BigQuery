# Step by step tutorial

Create a landing page. Add GTM and GA4. Publish the landing page on the internet using Firebase Hosting. 
Enable raw data from GA4 using BigQuery integration. 

**Min requirements / you will need access to:**
- A Google Cloud Platform project / Firebase console;
- Google Tag Manager;
- Google Analytics 4;

### 1. Prepare the landing page

Go to https://console.cloud.google.com/, select your project and Activate Cloud Shell then run:

```
git clone https://github.com/tailwindtoolbox/App-Landing-Page.git
cd App-Landing-Page
```

hit "Open Editor" and explore the landing.

### 2. Create Firebase Project

Go to https://console.firebase.google.com/ and hit "Add project", select your GCP Project or create a new one. Enable analytics -> Create a new account or select your GA account. Next and you ready.

### 3. Host the landing page on Firebase Hosting

Back to GCP Cloud Shell, just run:

```
firebase init 

// auth 
// select "Hosting: Configure files for Firebase Hosting" (with space) and Enter.
// select: use an existing project -> select your project
// What do you want to use as your public directory? public : hit enter
// Configure as a single-page app: hit y
// Set up automatic builds ... : hit N
```

```	
firebase deploy --only hosting
```

If everything goes fine you will receive a Hosting URL (click on that link : https://{gcp_project_id}.web.app

### 4. Setup Google Tag Manager

Go to: https://tagmanager.google.com and create a new account. 

Fill the name, country, container name and select web -> hit "Create" and accept GTM Terms of Service Agreement

You will receive a javascript snippet for gtm client side. Copy the code
and let's implement it to our landing.

### 5. Implement GTM and redeploy the landing page

Back on GCP Cloud Shell, hit "Open Editor" and select "index.html". 

You will copy the first snippet of gtm js code, and paste it as high in the <head> of the page as possible;

You will copy the second snippet of gtm nojs code, and paste it immediatly after the opening <body> tag;

Save and hit "Open Terminal", then redeploy your landing page.

```
firebase deploy --only hosting
```

Install Tag Assistant Legacy (by Google) extension for Chrome. Check if GTM it's running on your website (using Chrome -> Settings -> Developer Tools -> Network and reload the page) or using the Tag Assistant Legacy (by Google) extension.


### 6. Enable GTM + GA4 integration

Go to: https://analytics.google.com/ and select your Analytics Account. Go to "Admin" -> "Data Streams" -> "Add stream" -> "Web" and fill the form (Website url, Stream name and enable "Enhanced measurement"). At the end of the process you will receive the "Measurement ID" (copy this). 

Go to: https://tagmanager.google.com and select your Tag Manager Account. Go to "Tags" -> "New" -> hit "Tag Configuration" and choose "Google Analytics: GA4 Configuration" and fill the form (paste here the Measurement ID from the GA4 setup). Click on "Triggering" and choose "All pages". Give the tag a name and hit the "Save" button. 

Hit "Submit" and Publish the new GTM version.

### 7. Enable GA4 + BigQuery Integration

Go to: https://analytics.google.com/ and select your Analytics Account. Go to "Admin" -> "BigQuery Linking" -> "Link" -> "Choose a BigQuery project" and "Location" and hit "Next" -> then on "Frequency" choose what you need (pay attention because on "Streaming" you will have extra costs - check out documentation).

After some time (in our case one day) on GCP -> BigQuery we will have consolidate all the raw data from GA4


Enjoy it!
