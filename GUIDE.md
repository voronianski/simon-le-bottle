# Getting started with Facebook Messenger Platform

This walkthrough describes how to play with Facebook Messenger Platform in few easy steps.

### 1. Get the code

Start from cloning this repo and install all dependencies:

```bash
git clone git@github.com:voronianski/simon-le-bottle.git
cd simon-le-bottle
npm install
```

### 2. Create verify token

You'll need to put something as verify token environment variable into `package.json` start script in order to setup webhooks.

```json
"scripts": {
    "start": "APP_PAGE_TOKEN=\"0\" APP_VERIFY_TOKEN=\"YOUR VERIFY TOKEN\" node index.js"
},
```

### 3. Deployment

This example uses [NOW](https://zeit.co/now). It makes the process of deployment of node.js applications just a matter of running one word in command-line:

```bash
now
# ...deployment process
# returns url of the app 
# e.g. https://simon-le-bottle-udalkhaxub.now.sh
```

[NOW](https://zeit.co/now) is fast and serves under HTTPS which is important requirement in order to work with Messenger Platform. However it has several limitations currently:

- it generates new url on every deployment but doesn't support custom domains yet
- there's no way to see logs of the app yet

Though this [functionality will be added very soon](https://twitter.com/zeithq/status/720069484375969794) I advice to use [AWS Lambda functions](https://aws.amazon.com/lambda) with API Gateway if you would like to have full control of what's going on in the app.

### 4. Setup Facebook app and page 

Now you're ready to go to Facebook developers panel, create or use existing app (and page) and setup its' webhooks. [Please follow the steps from official quickstart guide](https://developers.facebook.com/docs/messenger-platform/quickstart). You don't need the code but other steps are necessary.

Your webhook url will look like `https://YOUR_GENERATED_URL.now.sh/webhook`.

![](https://scontent-frt3-1.xx.fbcdn.net/t39.2178-6/12057143_211110782612505_894181129_n.png)

### 5. Provide Page Access Token

You'll need to send Page Access Token to the app via request:

```bash
curl -i -H "Content-Type: application/json" -X POST -d "{\"verifyToken\": \"YOUR VERIFY TOKEN\", \"token\": \"YOUR PAGE ACCESS TOKEN\"} "https://YOUR_GENERATED_URL.now.sh/token" 
```

Now try to write something to your bot - it should answer with echoed messages just like on this gif image:

![](https://dl.dropboxusercontent.com/u/100463011/simon-le-bottle-demo.gif)

