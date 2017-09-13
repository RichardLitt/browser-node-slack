# node-slack

[![Greenkeeper badge](https://badges.greenkeeper.io/RichardLitt/browser-node-slack.svg)](https://greenkeeper.io/)

A node module for sending and receiving messages with Slack via webhooks that works with browserify.

[Slack](https://slack.com/) is a messaging platform that is easy to integrate with.
This module should be useful for creating various integrations with Slack, such as
chat bots!

## Install Slack

node-slack is available via npm:

```
npm i -S node-slack
```


Get your custom hook url from Slack by [setting up an integration](https://makeawesomeshit.slack.com/services/new/incoming-webhook).


```
var Slack = require('browser-node-slack');
var slack = new Slack('https://hooks.slack.com/services/EXAMPLEHOOK');
```

If your system requires that requests be made through
an HTTP or HTTPS proxy, you can either set an environment
variables https_proxy and http_proxy,
or pass in the optional second option:

```
var slack = new Slack(hook_url, {proxy: http_proxy});
```

To send a message, call slack.send:

```
slack.send({
	text: 'Howdy!',
	channel: '#foo',
	username: 'Bot'
});
```

You can also specify an emoji icon, a url to a custom icon, attachments,
and any of the other options listed [here](slack.com/services/new/incoming-webhook).


```
slack.send({
	text: 'Howdy!',
	channel: '#foo',
	username: 'Bot',
	icon_emoji: 'taco',
	attachments: attachment_array,
	unfurl_links: true,
	link_names: 1
});
```

To respond to an [outgoing webhook from slack](https://slack.com/services/new/outgoing-webhook), pass the information from the webhook into slack.respond,
along with a callback function responsible for returnign a response.

From inside an Express.js route, this is as easy as passing in req.body:

```
app.post('/yesman',function(req,res) {

	var reply = slack.respond(req.body,function(hook) {

		return {
			text: 'Good point, ' + hook.user_name,
			username: 'Bot'
		};

	});

	res.json(reply);

});

```
