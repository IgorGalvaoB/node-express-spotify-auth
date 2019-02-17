# node-express-spotify-auth
*Node Express app that handles token exchange for the Spotify Authorization Code flow*

> **Note**: For more information about Spotify Authorization, please visit https://developer.spotify.com/documentation/general/guides/authorization-guide/

## Create your Spotify App
Visit the Spotify developer portal (https://developer.spotify.com/) and create an application setting a CLIENT_ID, SECRET and CALLBACK_URI. 

`CLIENT_ID` - is generated by Spotify

`CLIENT_SECRET` - also generated by spotify

`CALLBACK_URI` - This Url should match the callback route of this hosted application 
  e.g (https://myspotauth/callback) or localhost:5000/callback for local development callbacks.

## Setting Env variables to match your App
There's a `.env` file provided containing the keys of required environment vars. 
Update this file with your App vars for local development.

There is an additional two env vars to be set:

`FINAL_URI` - This is the Url which will be loaded if authorisation and the token request is succesful. 
A spotify Token will be returned to this Url as a QueryString parameter. This token can be parsed and then used to in subsequent requests to the Spotify Api.

`STATEKEY` - The name given to the cookie used during auth. 
This doesn't require a change from `spotify_auth_state`

## Running locally
With the Env vars configured in a .env file, the app can be started locally `node index.js`

## Deploying the Express Application
The Express application to a Node.js environment such as Heroku, plese see above note about setting environment variables.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/bedechrissy/node-express-spotify-auth)

**Note**
Within Heroku, the environment vars are set via the CLI, for example: 

`heroku config:set CLIENT_ID=1234567809fdsnfj`


## Usage / flow
Once hosted, from another application you can:

* Redirect a user to the login route (https://myspotauth/login)
* A cookie will be stored locally and the user will be re-directed to the Spotify login page
* On succesful authentication, the callback Url will be called (https://myspotauth/callback)
* After checking everything ties up, a token request will be made
* If successful the user will be redirected to the FINAL_URL with a token in the Query string
* This token can be parsed and used to make subsequent requests to the Api

> **Note**: There is currently no functionality within this token swap for requesting Refresh tokens.
