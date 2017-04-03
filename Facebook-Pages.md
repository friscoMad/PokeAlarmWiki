## Overview
* [Prerequisities](#prerequisites)
* [Introduction](#introduction)
* [Basic Config](#basic-config)
  * [Required Parameters](#required-parameters)
  * [Example: Basic Alarm Configuration using Required Parameters](#example-basic-alarm-configuration-using-required-parameters)
* [Advanced Config](#advanced-config)
  * [Optional Parameters](#optional-parameters)
  * [Example: Alarm Configuration Using Optional Parameters](#example-alarm-configuration-using-optional-parameters)
* [How to get a Permanent Facebook Page Access Token](#how-to-get-a-permanent-facebook-page-access-token)

## Prerequisites
This guide assumes 

1. You are familiar with [JSON formatting](http://www.w3schools.com/json/default.asp)
2. You have read and understood the [Alarm Configuration](https://github.com/kvangent/PokeAlarm/wiki/Alarm-Configuration) Wiki
3. You are comfortable with the layout of `alarms.json`.

Please familiarize yourself with all of the above before proceeding.

## Introduction

**Facebook Pages** is an online social networking service that enables users to post status messages to a public profile specifically created for business, brands, celebrities, causes, and other organizations. Registered users can read and post messages, but those who are unregistered can only read them. Users access Facebook through the website interface, SMS or mobile device app.

PokeAlarm offers the following for Facebook Pages:

* Personalized notifications via [Dynamic Text Substitution](Dynamic-Text-Subsitution)

## Basic Config

### Required Parameters
These `alarms.json` parameters - `active`, `type`, and `page_access_token` - are required to enable the Facebook Pages alarm service:

| Parameters         | Description                            |
| --------------     |----------------------------------------|
| type               | must be `facebook_page`                |
| active             | `True` for alarm to be active          |
| page_access_token  | Your permanent FB page access token    |

### Example: Basic Alarm Configuration using Required Parameters
```json
{
	"active": "True",
	"type":"facebook_page",
	"page_access_token":"YOUR_PAGE_ACCESS_TOKEN"
}
```
**Note:** The above code is to be inserted into the alarms section of alarms.json. It does not represent the entire alarms.json file.

## Advanced Config

### Optional Parameters
In addition to the 3 required parameters, several optional parameters are available to personalize your Facebook Pages notifications.  Below is an example of these optional parameters and how they are incorporated into a functional alarm layout for Facebook Pages.

These optional parameters, `startup_message`, and `startup_list`, are entered at the same level as `"type":"facebookpages"`.

| Parameters         | Description                                                | Default                      |
|--------------------|------------------------------------------------------------|------------------------------|
| `startup_message`  | confirmation post when PokeAlarm initialized               | `True`                       |
| `startup_list`     | First post will list all alarmed pokemon enabled in `alarms.json`    | `True`            |

These optional parameters below are applicable to the `pokemon`, `pokestop`, and `gym` sections of the JSON file.
Check Image column to see where everything appears in the final publication.

![](images/Facebook.png)  

`pokemon` default values:

| Parameters       | Description                                       | Default                                       | Image|
| -----------------|---------------------------------------------------|-----------------------------------------------|----|
| `message`        | Message to post as status message                 | `A wild <pkmn> has appeared!`                                      | 1 |
| `link`           | Link to be added to notification text   		   | `<gmaps>` | Link |
| `image`        | Url of the image to show as a preview (False to show map preview)   | `https://raw.githubusercontent.com/kvangent/PokeAlarm/master/icons/<pkmn_id>.png` | 2 |
| `name`           | Link title (empty for linked page title)   		   | `<pkmn>`  | 3 |
| `description`    | Link description (empty for blank description)   		   | `Available until <24h_time> (<time_left>)`  | 4 |
| `caption`        | Link domain (empty for linked page domain)   		   | Empty  | 5 |


`pokestop` default values:

| Parameters       | Description                                       | Default                                       | Image|
| -----------------|---------------------------------------------------|-----------------------------------------------|----|
| `message`        | Message to post as status message                 | `Someone has placed a lure on a Pokestop!`                                      | 1 |
| `link`           | Link to be added to notification text   		   | `<gmaps>` | Link |
| `image`        | Url of the image to show as a preview (False to show map preview)   | `https://raw.githubusercontent.com/kvangent/PokeAlarm/master/icons/pokestop.png` | 2 |
| `name`           | Link title (empty for linked page title)   		   | `Lured Pokestop`  | 3 |
| `description`    | Link description (empty for blank description)   		   | `Lure will expire at <24h_time> (<time_left>)`  | 4 |
| `caption`        | Link domain (empty for linked page domain)   		   | Empty  | 5 |


`gym` default values:

| Parameters       | Description                                       | Default                                       | Image|
| -----------------|---------------------------------------------------|-----------------------------------------------|----|
| `message`        | Message to post as status message                 | `A Team <old_team> gym has fallen!`                                      | 1 |
| `link`           | Link to be added to notification text   		   | `<gmaps>` | Link |
| `image`        | Url of the image to show as a preview (False to show map preview)   | `https://raw.githubusercontent.com/kvangent/PokeAlarm/master/icons/gym_<team_id>.png` | 2 |
| `name`           | Link title (empty for linked page title)   		   | `<old_team> gym fallen`  | 3 |
| `description`    | Link description (empty for blank description)   		   | `It is now controlled by <new_team>`  | 4 |
| `caption`        | Link domain (empty for linked page domain)   		   | Empty  | 5 |



## Example: Alarm Configuration Using Optional Parameters
```json
{
	"active": "True",
	"type":"facebook_page",
	"page_access_token":"YOUR_PAGE_ACCESS_TOKEN",
	"startup_message":"True",
	"startup_list":"True",
	"pokemon":{
		"message": "<pkmn> available. <move_1>/<move_2> (<iv>% - <atk>/<def>/<sta>)",
		"link": "<gmaps>",
		"image" : "https://raw.githubusercontent.com/kvangent/PokeAlarm/master/icons/<pkmn_id>.png",
		"description": "Address: <address>",
            	"name": "<pkmn>"		
	},
	"pokestop":{
		"message": "Someone has placed a lure on a Pokestop! Lure will expire at <24h_time> (<time_left>).",
		"description": "Address: <address>",
		"link": "<gmaps>",
		"name": ""
	},
	"gym":{
		"message":"A Team <old_team> gym has fallen! It is now controlled by <new_team>.",
		"link": "<gmaps>",
            	"name": "<new_team>",
		"description": "Address: <address>",
		"image": "",
	}
}
```
**Note:** The above code is to be inserted into the alarms section of alarms.json. It does not represent the entire alarms.json file.

 
## How to get a Permanent Facebook Page Token

Use the [Graph API Explorer](https://developers.facebook.com/tools/explorer) for all of these steps except where otherwise stated.

### 0. Create Facebook App

**If you already have an app**, skip to step 1.

1. Go to [My Apps](https://developers.facebook.com/apps/).
2. Click "+ Add a New App".
3. Setup a website app.
4. Go to App Review of your new app and make sure your app is made Public.

### 1. Get User Short-Lived Access Token

1. Go to the [Graph API Explorer](https://developers.facebook.com/tools/explorer).
2. Select the application you want to get the access token for by clicking on the "Graph API Explorer" dropdown near the top right.
3. Click "Get Token" dropdown and choose "Get User Access Token".
4. In the pop-up, under the "Events, Groups & Pages" section, check "manage_pages" and "publish_pages".
5. Click "Get Access Token".
6. Grant access from a Facebook account that has access to manage the target page. Note that if this user loses access the final, never-expiring access token will likely stop working.

Token that appears in the "Access Token" field is your short-lived access token.

### 2. Generate Long-Lived Access Token

Following [these instructions](https://developers.facebook.com/docs/facebook-login/access-tokens#extending) from the Facebook docs, make a GET request to

`https://graph.facebook.com/v2.2/oauth/access_token?grant_type=fb_exchange_token&client_id={app_id}&client_secret={app_secret}&fb_exchange_token={short_lived_token}`

entering in your app's ID and secret, generated from step 0, and the short-lived token, generated in the previous step. Be sure to remove the curly braces "{}" when replacing values.

You **cannot use the Graph API Explorer**. For some reason it gets stuck on this request. I think it's because the response isn't JSON, but a query string. Since it's a GET request, you can just go to the URL in your browser.

The response should look like this:

`access_token=ABC123&expires=5182959`

"ABC123" will be your long-lived access token. You can put it into the [Access Token Debugger](https://developers.facebook.com/tools/debug/accesstoken) to verify. Under "Expires" it should have something like "2 months".

### 4. Get User ID

Using the long-lived access token, make a GET request to

`https://graph.facebook.com/v2.2/me?access_token={long_lived_access_token}`

Be sure to remove the curly braces "{}" when replacing values. The **id** field is your account ID. You'll need it for the next step.

### 5. Get Permanent Page Access Token

Make a GET request to

`https://graph.facebook.com/v2.2/{account_id}/accounts?access_token={long_lived_access_token}`

Be sure to remove the curly braces "{}" when replacing values. The JSON response should have a **data** field under which is an array of items the user has access to. Find the item for the page you want the permanent access token from. The **access_token** field should have your permanent access token. Copy it and test it in the [Access Token Debugger](https://developers.facebook.com/tools/debug/accesstoken). Under "Expires" it should say "Never".

