# gatsby-plugin-cookiehub-banner

Gatsby plugin to use cookie banner generated with cookiehub.

This plugin works in an easy way together with a plugin to add google analytics GDPR compliant: [gatsby-plugin-google-analytics-gdpr](https://github.com/VirtualFox0/gatsby-plugin-google-analytics-gdpr)

## Setup

* Create [CookieHub](https://www.cookiehub.com/) account.
* [Add widget](https://www.cookiehub.com/widgets).
* Configure widget at least with appropriate categories in the category tab.

## Install

`npm install --save gatsby-plugin-cookiehub-banner`

## How to use

```javascript
// In your gatsby-config.js
module.exports = {
  plugins: [
    {
        resolve: `gatsby-plugin-cookiehub-banner`,
        options: {
            // Your cookiehub widget ID. You can find the widget ID in the CookieHub tab "Your script" of the appropriate widget. The ID is part of the CookieHub URL: https://cookiehub.net/cc/YOUR_COOKIEHUB_ID.js
            cookieHubId: "YOUR_COOKIEHUB_BANNER_ID",
            // Categories configured with CookieHub
            categories: [
            { 
                categoryName: 'analytics', // Unique id of the category which you can set in CookieHub categories.
                cookieName: 'gatsby-plugin-google-analytics-gdpr_cookies-enabled' // Custom cookie name
            },
            { 
                categoryName: 'marketing',
                cookieName: 'marketing-enabled'
            }
            ]
        }
    },
  ],
}
```
## How it works
The plugin embeds the script generated by CookieHub to show the cookie banner. 
On CookieHub initialization and on user input the plugin sets one cookie per category. Depending on the user input the value should be `true` or `false`. 
You can configure your categories in the `gatsby-config.js` with the according cookie names.

Cookie Handling Example: 
If you want to integrate Google Analytics, you can start tracking as soon as the analytics cookie is set to `true` and disable tracking if the user withdraws the choice.

There is a GDPR plugin to use Google Analytics in an easy way with this plugin: [gatsby-plugin-google-analytics-gdpr](https://github.com/VirtualFox0/gatsby-plugin-google-analytics-gdpr). Install and configure the `gatsby-plugin-google-analytics-gdpr` plugin and set the analytics category cookie name to `gatsby-plugin-google-analytics-gdpr_cookies-enabled`.

## Options

### `cookieHubId`

Your cookiehub widget ID. You can find the widget ID in the CookieHub tab "Your script" of the appropriate widget. The ID is part of the CookieHub URL: https://cookiehub.net/cc/YOUR_COOKIEHUB_ID.js

### `categories`

Define your categories configured with CookieHub. A category consists of `categoryName` and `cookieName`. 

#### `categoryName`

Unique id of the category which you can set in CookieHub categories.

#### `cookieName`

Define a custom cookie name. If none cookieName is given, the plugin will generate one.
