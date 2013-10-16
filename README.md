#Ark API doc


* [Get profile with email] (#email)
* [Get profile with network] (#network)
* [Batch process] (#batch)

<a name="email" />
## Get profile with email

Receive a full profile for given email.

* Method: GET
* Auth: YES
* Url: https://testapi.ark.com/email/[email]

__Response codes__

* 200, profile is retrieved in JSON format.
* 302, Profile is being retrieved perform another request after a few seconds.
* 404, There is no info available about this profile.
* 401, Unauthorized, token missing or incorrect.
* 429, Out of requests, current token has no more request left.
* 503, Internal server error. Retry after a few minutes.

__Headers__

* apit_token - Your API token.

__Example__

```js
var request = require('request');

request(
		{
			url : 'https://testapi.ark.com/email/goofyahead@gmail.com',
			headers : {
				api_token : 'your_token_goes_here'
			}
		},
		function (err, response, body) {
			if (err) throw err;
			console.log(body); //response object is printed
		});
```

__Response__

```js
{"name":"Alejandro Vidal","languages":[],"pics":["http://qph.cf.quoracdn.net/main-thumb-11185184-200-2fVaPQE11v5L7i010YLWteYg9cbK59vO.jpeg","http://a0.twimg.com/profile_images/1089161969/yo_normal.jpg","http://a0.twimg.com/profile_images/1089161969/yo_reasonably_small.jpg","http://a0.twimg.com/profile_images/1089161969/yo.jpg"],"emails":[],"links":[{"name":"Twitter","link":"http://twitter.com/goofyahead"},{"name":"Quora","link":"http://www.quora.com/Alejandro-Vidal"}],"education":[],"work":[],"interests":{"other":["Ruby","Ruby on Rails"]}}
```

A profile that contains all the profile information.

{{Collapse|1=Discussion text to be put into box.|bg=#F0F2F5}}
All the documentation to work with our api and code snippets.
