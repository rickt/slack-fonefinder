# slack-team-directory-bot
##### overview
golang backend for a super-handy Slack `/slash` command that searches the team directory. i install as `/dir`. example use:

user enters: `/dir ric`

response that users sees: 

```
Your Company Team Directory Bot [04:41] Only you can see this message
   rick tait: :phone: (213) NNN-NNNN :email: rickt@REDACTED.com :slack: @rickt
   Richard Richardson: :phone: (213) NNN-NNNN :email: richard@richardso.com :slack: @richard
```

# ☎ slack-team-directory-bot
backend basics: 
* you configure a slack `/slash` command to POST to URI `/slack` with appropriate payload `token=TOKEN` and `text=SEARCHSTRING`
* the best match & phone number is returned to the user
* if the expected Slack "challenge" token (get this from your `/slash` command setup) is not sent along with the request, the request is dropped
* requires a separate Slack OAuth2 bearer token (get a quickie from https://api.slack.com/docs/oauth-test-tokens) to establish backend connection into your Slack to retrieve user data & POST response to request into Slack
* both tokens are configured as environment variables in the app.yaml

written specifically to run in Google App Engine. should be plug-n-play for you. 

1. deploy to App Engine using `goapp deploy` once you've setup goapp
2. setup your `/slash` command in Slack
3. profit

##### notes
* this is written specifically for google app engine, hence no main() and  [github.com/rickt/slack-appengine](https://github.com/rickt/slack-appengine) requirement
* change values as appropriate in the environment variable section in your app.yaml

##### testing
* Overview:
```
$ curl https://fonefinderzu.appspot.com/slack -XPUT --data "token=REDACTED&text=john"`
```
* Example run:
```
$ curl https://fonefinderzu.appspot.com/slack -XPUT --data "token=REDACTED&text=tait"
{"channel":"","username":"","text":"rick tait: :phone: (213) NNN-NNNN :email: \u003cmailto:rickt@redacted.com|rickt@redacted.com\u003e :slack: \u003c@REDACTED|rickt\u003e\n","response_type":"","icon_emoji":"","u
nfurl_links":false,"attachments":null}
```

##### demo
this app is currently up & running at [fonefinderzu.appspot.com](http://fonefinderzu.appspot.com/slack)
