# slack-fonefinder
##### overview
golang backend for a super-handy Slack /slash command that searches the team directory. called from slack via /slash command. i install as "/ff". example use:

enter: /ff rickt

response: Fone Finder BOT [04:41] Only you can see this message
          rick tait: :phone: (213) NNN-NNNN :email: rickt@REDACTED.com :slack: @rickt

# ☎finder
installed as "/ff" in slack. POST to URI "slack" with appropriate payload "token=TOKEN" and "text=SEARCHSTRING". returns the best match & phone number to the user. if the expected Slack challenge token is not sent along with the request, the request is dropped. tokens are configured as environment variables in the app.yaml. a separate Slack token is required to POST back into Slack. 

written specifically to run in Google App Engine. should be plug-n-play for you. 

1) deploy to App Engine using "goapp deploy" once you've setup goapp
2) setup your /slash command in Slack
3) profit

##### notes
* this is written specifically for google app engine, hence no main() and  [github.com/rickt/slack-appengine](https://github.com/rickt/slack-appengine) requirement
* change values as appropriate in the environment variable section in your app.yaml

##### testing
$ curl https://fonefinderzu.appspot.com/slack -XPUT --data "token=REDACTED&text=john"

##### demo
this app is currently up & running at [fonefinderzu.appspot.com](http://fonefinderzu.appspot.com/slack)
