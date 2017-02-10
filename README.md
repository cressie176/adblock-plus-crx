# Adblock-Plus.crx

Adverts can slow and even break functional tests. If you run your functional tests using ChromeDriver you can install extensions like AdBlock-Plus as follows...

```
{
  ...
  "desiredCapabilities": {
    "javascriptEnabled": true,
    "acceptSslCerts": true,
    "browserName": "chrome",
    "chromeOptions": {
      "args": [ "no-sandbox" ],
      "extensions": [ "Q3Iy....AAAA=" ]
    }
  }
  ...
}
```
Where ```Q3Iy....AAAA=``` is the base64 encoded crx file you want to install. Unfortunately Adblock-Plus is around 600KB when encoded and not something you really want to include in a json file.

When using the excellent [Nightwatch.js](http://nightwatchjs.org/) you can define configuration in ```nightwatch.conf.js``` instead of json.

```
var adBlockPlus = require('adblock-plus-crx')

module.exports = {
  ...
  "desiredCapabilities": {
    "javascriptEnabled": true,
    "acceptSslCerts": true,
    "browserName": "chrome",
    "chromeOptions": {
      "args": [ "no-sandbox" ],
      "extensions": [ adBlockPlus.base64() ]
    }
  }
  ...
}
```
# Modifications
AdBlock-Plus opens a new tab on first run and since WebDriver tests typically start with a fresh profile each run gets more than a little annoying.  We've disabled first run behaviour by setting ```suppress_first_run_page``` to true and recreating the crx.

# How do make your own crx (instructions for OSX)
1. For this project
1. Update the adblock-plus-crx version in package.json
1. Add modifications to ```./scripts/update.sh```
1. Run ```./scripts/update.sh``` from forks root directory (the one containing package.json)
1. Commit your changes but don't submit a pull request (I won't trust a generated crx)
