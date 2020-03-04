# Whole Whale GTM Basic Formula with Lighthouse and Politweets

This file is meant to be a ready-set starting point to set basic analytics tracking on your site through Google Tag Manager, as well as implementing the script from [Lighthouse by Whole Whale](https://www.wholewhale.com/products/lighthouse) which helps you track special visitors on your site and [Politweets by Whole Whale](https://www.wholewhale.com/products/politweets) which helps your visitors, donors, and supporters to reach out to their representatives through Tweeter on the subjects that matter most to your cause.
 
## Installation

Download the .json file.   
In Google Tag Manager:
* Click the Admin tab in your GTM container
* Click `Import Container`
* Click `Choose Container File` and select the .json file
* Under `Choose a workspace`, select existing and select your default workspace
* Under `Choose an import option`, select `merge`
* Select `rename conflicting tags` if your container is not empty
* Click *confirm*

You are now ready to customize and use the tags. Preview and edit as needed.    

To make sure politweets is on your site properly, you will also need to place the html `<div>` element provided by [the politweets app](https://app.politweets.org/campaigns) in the location that you will like the widget to appear on the page, the snippet should look something like so:
```
<div id="wholewhale-polytweet-main" campaign_id="0b000cf0-0000-0000-00fd-cec00000e000" pid="00b0e00d-00fc-0d0e-0e0e-000efe0e00ab"></div>
``` 

## Formula Contents

### Variables

* Google Analytics Settings:  
*You will need to add your Google Analytics property ID* which is necessary since it is already connected to the currently existing tags. This variable is a reusable option to not have to rewrite any general settings that your tag would share with others. - If you create a tag where you will need to change any of this general settings, within the tag options you can check the `Enable overriding settings in this tag` section which will allow you to update those settings for the individual tag only
* PII Scrubber & Lighthouse Custom Dimension: (*Not necessary for everyone. If you know or you believe you have Personal Identifiable Information being passed any of the URL paths of your site, this variable will rid of it*)
You will need to edit the code by replacing `?!youremail\.com` and `?youremail\.com` with the domain name of your site's email (make sure to keep the back slash before the dot). as well as changing the number in front of `var clientIdIndex =` on line 10 (**this should the number of your custom dimension created for lighthouse in your Google Analytics account settings.** [For more information on Lighthouse set up for custom dimesion](https://www.wholewhale.com/lighthouse/setup/#segments))  
**_NOTE_**: If you do not have any PII, edit the Google Analytics Settings variable. Under "more settings" > "fields to set" switch the value currently set to `{{PII Scrubber + Lighthouse Custom Dimension}}` for `{{Custom Dimension- Lighthouse}}` and edit the **Custom Dimension- Lighthouse** variable to hold the dimension index number that was generated when created in GA. (*this field in the settings variable is necessary for the proper function of the lighthouse set up*)

### Triggers
Triggers are like sensors (commonly called "listeners")whose sole job is to check if an action has been performed on site and let GTM know that the tags related to that trigger can be executed. Each Trigger relates to an action and contains certain requirements in order to fire (called "rules").

* 15 Second Timer: Fires if a visitor has been on the site for at least 15 seconds
* All Clicks: Fires if anything on the page has been clicked
* All Links: Fires if any link has been clicked
* All Outbound Links: Fires if any link to an external site has been clicked(so, any link that does not contain your website's hostname).  
_For this to properly work, you will need to update the second rule under `the trigger fires on` where it says `yoursite.org`. You will need to change it for your site's hostname_
* Form Submissions: Fires if a form has been properly filled out and submitted
* PDF Click: Fires on clicks to PDF downloadable content
* Scroll Depth: Fires when users reach difenrent percentage ranges through the page

### Tags* Adjusted Bounce Rate
```
Category: visit
Action: 15 Seconds
Label: {{Page Path}}
```
* All Link Tracking
```
Category: Link Clicks
Action: Page: {{Page URL}}
Label: Link: {{Click URL}} - {{Click Text}}
```
* Click Tracking
```
Category: All Clicks
Action: Text: {{Click Text}}
Label: Link: Page: {{Page URL}}
```
* Google Analytics Pageview
* Outbound Links
```
Category: Outbound Links
Action: Click
Label: {{Click URL}}
```
* PDF Downloads
```
Category: Download
Action: PDF
Label: {{Click URL}}
```
* Scroll Depth 
```
Category: Scroll Depth
Action: Percentage: {{Scroll Depth Threshold}}
Label: Page URL: {{Page URL}}
```
* Lighthouse   
`Add the User ID, Identity ID, and API Key found in the script code provided in your Lighthouse account`
* Politweets

