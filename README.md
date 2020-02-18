# Whole Whale GTM Basic Formula with Lighthouse and Politweets

The file is meant to be a ready-set starting point to set basic analytics tracking on your site through Google Tag Manager as well as implementing the script from [Lighthouse by Whole Whale](https://www.wholewhale.com/products/lighthouse) which helps you track special visitors from your site and [Politweets by Whole Whale](https://www.wholewhale.com/products/politweets) which helps your visitors, donors, and supporters to reach out to their representatives through Tweeter on the subjects that matter most to your cause.
   
## Formula Contents

### Variables

* Google Analytics Settings: 
You will need to add your Google Analytics(GA) property ID. Already connected to the currently existing tags, it is a reusable option to not have to rewrite any general settings that your tag would share with others
* PII Scrubber & Lighthouse Custom Dimension:
You will need to edit the code by replacing `?!youremail\.com` and `?youremail\.com` with the domain name of your sites email (make sure to keep the back slash before the dot). as well as changing the number in front of `var clientIdIndex =` on line 10 for the number of your custom dimension created for lighthouse in Google Analytics settings. [For more information on Lighthouse set up for custom dimesion](https://www.wholewhale.com/lighthouse/setup/#segments)
to use this variable, edit the Google Analytics Settings variable. Under "more settings" > "fields to set" add a field and fill in `customTask` under name, and `{{PII Scrubber + Lighthouse Custom Dimension}}`under value.
**_NOTE_**: If you do not have any PII use the `{{Custom Dimension- Lighthouse}}` variable as the value and edit the **Custom Dimension- Lighthouse** variable to hold the dimension index number that was generated when created in GA.

### Triggers
If not very acquainted with GTM. Triggers are like sensors (commonly called "listeners")whose solely job is to check if an action has been performed on the page by a visitor and let GTM know that the tags related to it can be executed. Each Trigger relates to an action and it contains certain requirements for it to accept it (called "rules").

* 15 Second Timer: It checks if a visitor has been on the site for 15 seconds
* All Clicks: It checks if anything on the page has been clicked
* All LinksL: It checks if any links have been clicked
* All Outbound Links: it checks if any links outside of the site (AKA that have a different hostname)
* Form Submissions: it checks if a form has been filled and sent
* PDF Click: Checks on clicks to PDF downloadable content
* Scroll Depth: It listents for difenrent percentage ranges that the user had scrolled through the page

### Tags
* Adjusted Bounce Rate
`Category: visit
Action: 15 Seconds
Label: {{Page Path}}`
* All Link Tracking
`Category: Link Clicks
Action: Page: {{Page URL}}
Label: Link: {{Click URL}} - {{Click Text}}`
* Click Tracking
`Category: All Clicks
Action: Text: {{Click Text}}
Label: Link: Page: {{Page URL}}`

* Google Analytics Pageview

* Outbound Links
`Category: Outbound Links
Action: Click
Label: {{Click URL}}`
* PDF Downloads
`Category: Download
Action: PDF
Label: {{Click URL}}`
* Scroll Depth 
`Category: Scroll Depth
Action: Percentage: {{Scroll Depth Threshold}}
Label: Page URL: {{Page URL}}`
* Lighthouse
`Add the User ID, Identity ID, and API Key found in the script code provided in your Lighthouse account.`
* Politweets

## Installation

After downloading the .json file, under the Admin tab within the GTM container, click `Import Container`, click `Choose Container File` and grab the .json file, then select `existing`, select your default works space, and keep `merge` as the option checked, select rename conflicting tags if your container is not empty and click confirm.

You are now ready to use the tags. Preview and edit as needed. 

To make sure politweets is on your site properly, you will need to also need to place the html `<div>` element provided by [the politweets app](https://app.politweets.org/campaigns) in the location that you will like it to appear on the page, the snippet should look something like so:
```
<div id="wholewhale-polytweet-main" campaign_id="0b000cf0-0000-0000-00fd-cec00000e000" pid="00b0e00d-00fc-0d0e-0e0e-000efe0e00ab"></div>
```
