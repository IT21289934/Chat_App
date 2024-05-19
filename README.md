# Chat_App


## Getting Started

To run this example, run the following commands:

```bash
git clone https://github.com/IT21289934/Chat_App
cd Chat_App
```

```shell
okta register
```

If you already have a developer account, use `okta login` to integrate it with the Okta CLI. 

Provide the required information. Once you register, create a client application in Okta with the following command:

```shell
okta apps create
```

You will be prompted to select the following options:
- Type of Application: **2: SPA**
- Redirect URI: `http://localhost:8080/login/callback`
- Logout Redirect URI: `http://localhost:8080`

The application configuration will be printed to your screen:

```shell
Okta application configuration:
clientId: '0oah6iem87H4kKcKU5d7',
issuer: 'https://dev-18205685.okta.com/oauth2/default'
```

You will also need to generate a token so that your chat server can communicate with the Okta authentication service. Run `okta login`, open the resulting URL in your browser, sign-in, and navigate to **Security > API**.

Select the **Tokens** tab. Click on **Create Token** and type in a name for the token. In the following popup, you will be shown the token that has been generated. 

Replace the values in `chat-server/chat.js` with these values.

```js
const jwtVerifier = new OktaJwtVerifier({
  clientId: '{yourClientID}',
  issuer: 'https://{yourOktaDomain}/oauth2/default',
});

const oktaClient = new okta.Client({
  orgUrl: 'https://{yourOktaDomain}',
  token: '{yourOktaAPIToken}',
});
```

Update `chat-client/.env` with your Okta settings too.

```dotenv
PORT=8080
REACT_APP_OKTA_ORG_URL=https://{yourOktaDomain}
REACT_APP_OKTA_CLIENT_ID={yourClientID}
```

If you haven't done so already, install the dependencies.

```shell
cd chat-server
npm install

cd chat-client
npm install
```

Start the chat server in one terminal window with `npm start`, and the chat client in another window.

```shell
npm start
```

Open `http://localhost:8080` in your favorite browser and you should be able to log in.

