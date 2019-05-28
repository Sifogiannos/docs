## Quick Guide

1.  Create the pollfishConfig object to setup Pollfish library
2.  Include jQuery library to your website (version 1.4.3 and above)
3.  Include Pollfish library to your website
4. Request your account to get verified from Pollfish Dashboard


Pollfish library works with IE 10 and above, Chrome 16 and above, Firefox 20 and above.
You can checkout the Pollfish Webplugin experience by visiting this page [here](/webplugin).

## Requirements

- jQuery version 1.4.3 and above

### Developer Vs Release Mode

You can use Pollfish either in Developer or in Release mode.  

*   Developer mode is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
*   Release mode is the mode to be used for a released app in a live online website(start receiving paid surveys).

If you **do not set the debug parameter in your Pollfish config object**, Pollfish runs in release mode by default so it is **IMPORTANT** when you are in development that **YOU MUST** set debug to true in order to be able to receive development surveys.  

**Note: Be careful to turn the debug parameter to false when you put your website online!!**

## Steps Analytically

### 1\. Obtain a Developer Account in Pollfish

Register at [www.pollfish.com](//www.pollfish.com) as a Developer.

### 2\. Add new app in Pollfish panel and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com) and add a new app at Pollfish panel in section My Apps and copy the given API key for this app to use later in your pollfishConfig object in your app.

### 3\. Set up the pollfishConfig object

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  debug: true
};
```

**IMPORTANT: Pollfish will autostart serving surveys once the polfishConfig object is set, with a valid api key.**

#### pollfishConfig object takes the following parameters:

1.  <span class="params">api_key (required)</span>  
    Your API Key (from step 2)
2.  <span class="params">indicator_position (optional)</span>  
    The Position where you wish to place the Pollfish indicator.  
    There are four different positions: {TOP_LEFT, BOTTOM_LEFT, TOP_RIGHT, BOTTOM_RIGHT}  
    Defaults to BOTTOM_RIGHT
3.  <span class="params">uuid (optional)</span>  
    Uuid for callback to your server  
4.  <span class="params">debug (optional)</span>  
    Sets Pollfish in debug mode  
    Set true to enable debug mode (for development), set false to set Pollfish in release mode.  
    Defaults to false
5.  <span class="params">offerwall (optional)</span>  
    Sets Pollfish in offerwall approach mode  
    Set to true to enable offerwall mode
    Defaults to false
6.  <span class="params">survey_format (optional)</span>  
    Works only in debug mode  
    This parameter is used during development to check integration with different survey formats.
    Acceptable values are (defaults to 0):
    
    - Basic: 0
    - Playful: 1
    - Random: 2
    - 3rd-party: 3
7.  <span class="params">rewardName (optional)</span>

    Sets reward name parameter to Pollfish. You can set your own coin/point/reward name for when your respondents complete a       survey
8.  <span class="params">rewardConversion (optional)</span>

    Sets reward conversion parameter to Pollfish. You can set your own conversion value for when your respondents complete a       survey. The conversion expects a string and it should contain the number of rewards the respondent will receive for every 
    dollar being payed. In example, when a survey has a CPA of 30 and a conversion of 50. Then the rewardValue property will       contain the value '15'.

Below you can see an example of the pollfishConfig object:  

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  indicator_position: "BOTTOM_RIGHT",
  debug: true,
  offerwall: false,
  uuid: "string_uuid"
};
```

### Other pollfishConfig object callback options (optional)

Pollfish Webplugin provides some callback functions to call when specific actions are executed in the Pollfish survey.

#### pollfishConfig object takes the following optional callback function parameters:

1.  <span class="params">closeCallback</span>  
    Called when user clicks or touches outside the Pollfish survey container, or if he clicks or touches the close icon
2.  <span class="params">userNotEligibleCallback</span>  
    Called when the user is not eligible for surveys
3.  <span class="params">closeAndNoShowCallback</span>  
    Called when the survey is closed and the indicator hides permanently (e.g. when finishing the survey)
4.  <span class="params">surveyCompletedCallback</span>  
    Called when the user finishes the survey. Also contains revenue, survey format, estimated LOI, [survey_class](https://www.pollfish.com/docs/api-documentation) (surveyProvider + type) and IR survey information on offerwall integrations.
5.  <span class="params">surveyAvailable</span>  
    Called when there is an availble survey for the user. Also contains revenue, survey format, estimated LOI, [survey_class](https://www.pollfish.com/docs/api-documentation) (surveyProvider + type) and IR survey information. 
6.  <span class="params">surveyNotAvailable</span>  
    Called when there is no available survey for the user

Below you can see an example of the pollfishConfig object with all possible callbacks:  

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  indicator_position: "BOTTOM_RIGHT",
  debug: true,
  offerwall: false,
  uuid: "string_uuid",
  alwaysReturnContent: false, // show the iframe even when no survey is found
  closeCallback: customSurveyClosed,
  userNotEligibleCallback: customUserNotEligible,
  closeAndNoShowCallback: customCloseAndNoShow,
  surveyCompletedCallback: customSurveyFinished,
  surveyAvailable: customSurveyAvailable,
  surveyNotAvailable: customSurveyNotAvailable,
  rewardName: 'Diamonds',
  rewardConversion: '50', // 1 USD = 50 Diamonds, ie: if survey cpa is 30, then it will return 15 diamonds
};

function customSurveyClosed(){
  console.log("user closed the survey");
}

function customUserNotEligible(){
  console.log("user is not eligible");
}

function customSurveyFinished(){
  console.log("user finished the survey");
}

function customCloseAndNoShow(){
  console.log("close and hide the indicator");
}

function customSurveyAvailable(data){
  console.log(`
      pollfish survey is available with revenue: ${data.revenue},
      survey format playful: ${data.playful},
      survey_loi: ${data.survey_loi},
      survey_ir: ${data.survey_ir},
      survey_class: ${data.survey_class},
    `);
}

function customSurveyNotAvailable(){
  console.log("survey not available");
}
```

### 4\. Include the necessary files in your website

Include the jQuery library with version greater or equal than 1.4.3 if it's not already included, as the example below:

```html
<!-- Include jQuery library >= 1.4.3 version -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
```

Then include the Pollfish Webplugin, as the example below:

```html
<!-- Include Pollfish Webplugin -->
<script src="https://storage.googleapis.com/pollfish_production/sdk/webplugin/pollfish.min.js"></script>
```

**IMPORTANT: Keep in mind that you should include the Pollfish Webplugin after the pollfishConfig object, like the example below:**

```html
<!-- Initialize your pollfishConfig object first -->
<script>
  var pollfishConfig = {
    api_key: "api_key_goes_here",
    debug: true
  };
</script>

<!-- Then include Pollfish Webplugin -->
<script src="https://storage.googleapis.com/pollfish_production/sdk/webplugin/pollfish.min.js"></script>
```

### 5\. Launch Pollfish Webplugin explicitly

You can trigger Pollfish Webplugin explicitly at any given moment and ignore the autostart functionality. In order to ignore autostart, you need to set the ready optional callback function on the pollfishConfig object, as the example below:

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  debug: true,
  ready: pollfishReady
};

function pollfishReady(){
  //Pollfish Webplugin is ready, so you can call it excplicitly using the Pollfish.showIndicator or Pollfish.showFullSurvey functions
}
```

After the ready callback is called, you can either show the indicator or open the full survey panel, as described in the next section.

### 6\. Show & hide Pollfish Webplugin explicitly

**Show the Pollfish Indicator that the user has to click in order to see the full survey**  

```js
Pollfish.showIndicator();
```

**Show the full survey so that the user can respond immediately**  

```js
Pollfish.showFullSurvey();
```

_If you call Pollfish.showIndicator or Pollfish.showFullSurvey and there is no available survey, they will return false._

**Hide the indicator and the full survey**  

```js
Pollfish.hide();
```

#### 7\. Explicitly requesting a specific survey format for testing purposes (works only in debug mode)

If you want to test Pollfish different available Survey Formats you can set survey_format as descibed in Section 3.

| **Note:** You can request and receive a specific survey format only in debug mode

Here is an example of how you can select a Playful Survey Format.

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  indicator_position: "BOTTOM_RIGHT",
  debug: true,
  survey_format: 1
};
```
<br/>
*Both in production and during testing 3rd-party surveys when a survey is completed or the user gets screened out, since the user is outside of the website in another browser tab, the next time Pollfish will be called within the website, survey completed or user not eligible event will be fired (instead of survey received or not available) in order to inform the user on what happened at the website.
<br/>

One way to approach this is to listen for the focus event and call Pollfish.start like in the example below:

```js
document.querySelector('body').onfocus = function () {
  Pollfish.hide();
  Pollfish.start(pollfishConfig);
};
```

Another way is to wait for the next session of the user and Pollfish will notify you about those events.


#### 8\. Explicitly Show the "No Survey Found" page when no survey is found

The default behavior when there is no survey found, is to not show anything to the user, and no indicator is shown.
If this is not the required behavior for your use case you can set the `alwaysReturnContent` set to `true` and the indicator will always be shown, even when no survey can be answered.

```js
const config = {
  // ...,
  alwaysReturnContent: true
  // ...,
}
```

## Update your Privacy Policy

We invite you to check and comply with the respondent’s terms of use. Pollfish webplugin uses cookies to uniquely and anonymously identify users.  


### Add the following paragraph to your app's privacy policy

*“This website uses Pollfish web plugin. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones and website owners in order to have access to users of such applications/websites and address survey questionnaires to them. This website uses and enables Pollfish cookies. When a user connects to this website, Pollfish detects whether the user is eligible for a survey. Data collected by Pollfish will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. For a full list of data received by Pollfish through this website, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. By using this website you accept this privacy policy document and you hereby give your explicit consent for the placement of a Pollfish cookie in your system and the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website or by disabling “third party cookies” from your browser’s settings. We once more invite you to check the Pollfish respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*

*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”*

<br/><br/><br/>

| **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process users need to go through in order to join the platform. Bear in mind that if a paid survey is available at that point of time, the demographic questions will be inserted at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this new type of targeting.

<br/>

<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>
<br/>


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 


<br/>
You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>

<br/>


##  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>

<br/>

<br/>
