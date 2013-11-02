#Ark API doc

All the documentation to work with our api and code snippets.

* [Get profile with email] (#email)
* [Get profile with network] (#network)
* [Batch process] (#batch)
* [Response example] (#example)

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

* api_token - Your API token.

__Example__

```js
var request = require('request');

request(
		{
			url : 'https://testapi.ark.com/email/goofyahead@gmail.com',
			headers : {
				api_token : 'c29d1b9f-5ecd-49e5-8f39-ee4c8c7d4dc4'
			}
		},
		function (err, response, body) {
			if (err) throw err;
			console.log(body); //response object is printed
		});
```

<a name="network" />
## Get profile with network handle

Receive a full profile for given network.

* Method: GET
* Auth: YES
* Url: https://testapi.ark.com/network/[network]:[ID]

__Response codes__

* 200, profile is retrieved in JSON format.
* 302, Profile is being retrieved perform another request after a few seconds.
* 404, There is no info available about this profile.
* 401, Unauthorized, token missing or incorrect.
* 429, Out of requests, current token has no more request left.
* 503, Internal server error. Retry after a few minutes.

__Headers__

* api_token - Your API token.

__Example__

```js
var request = require('request');

request(
		{
			url : 'https://testapi.ark.com/network/fb:Alejandro.Vidal.Rodriguez',
			headers : {
				api_token : 'c29d1b9f-5ecd-49e5-8f39-ee4c8c7d4dc4'
			}
		},
		function (err, response, body) {
			if (err) throw err;
			console.log(body); //response object is printed
		});
```

__Networks that can be searched__

* Facebook, fb
* Twitter, tw

<a name="batch" />
## Get a batch response

Receive an object on a callback URL with the results.
This is a backend to backend request.
There is a limit of 100 profiles per batch.

* Method: POST
* Auth: YES
* Url: https://testapi.ark.com/batchprofile

__Response codes__

* 200, profile is retrieved in JSON format.
* 302, Profile is being retrieved perform another request after a few seconds.
* 404, There is no info available about this profile.
* 401, Unauthorized, token missing or incorrect.
* 429, Out of requests, current token has no more request left.
* 503, Internal server error. Retry after a few minutes.

__Headers__

* api_token - Your API token.
* callback_url: [the URL you want to be called when processed]


__Body__
```js
[
{"type" : "email", "id" : "email@domain.com"}, 
{"type" : "network", "id" : "fb/profileID"}
]
```
__Example__

```js
var request = require('request');

request(
{
	url : config.testUrl + '/batchprofile',
	strictSSL : false,
	method: 'POST',
	headers: {
		api_token : testToken,
		callback : 'http://myserver.com/arkcallback'
		},
	json : {
		type : 'email', id: 'goofyahead@gmail.com',
		type : 'email', id: 'patrick@ark.com',
		type : 'email', id: 'inventionasdf@inventedasdfasdf.com'
		}
},
	function (err, response, body) {
		if (err) throw err;
		console.log(body);// this will show the callback url where the results will be sent
	});
```


<a name="example" />
## Response example and format

```js
{
  "name": "Alejandro Vidal Rodriguez",
  "location": "Madrid Area, Spain",
  "pics": [
    "https://secure.gravatar.com/avatar/cd351ae83b3a49c828bc6b4b5320844e?s=80&d=404",
    "http://m.c.lnkd.licdn.com/mpr/mpr/p/1/000/1e8/1df/131669a.jpg",
    "https://s3.amazonaws.com/photos.angel.co/users/228359-medium_jpg?1358867761",
    "http://www.gravatar.com/avatar/cd351ae83b3a49c828bc6b4b5320844e?d=http%3A%2F%2Fb.vimeocdn.com%2Fimages_v6%2Fportraits%2Fportrait_100_gray.png&s=100",
    "http://lh5.googleusercontent.com/-4FIoLR71zJs/AAAAAAAAAAI/AAAAAAAAAAA/uio2xBeZjDw/photo.jpg",
    "http://profile.ak.fbcdn.net/hprofile-ak-ash3/1017492_10151598447722455_952834597_n.jpg",
    "http://a.vimeocdn.com/images_v6/portraits/portrait_100_gray.png",
    "http://a.vimeocdn.com/images_v6/portraits/portrait_75_gray.png",
    "http://a.vimeocdn.com/images_v6/portraits/portrait_300_gray.png",
    "http://a.vimeocdn.com/images_v6/portraits/portrait_30_gray.png",
    "http://profile.ak.fbcdn.net/hprofile-ak-ash3/1044013_10151445458302455_2104871098_n.jpg",
    "https://secure.gravatar.com/avatar/cd351ae83b3a49c828bc6b4b5320844e?s=400&d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-user-420.png",
    "https://secure.gravatar.com/avatar/24560b2e25770a2ce7d207292ab5bafb?s=80&d=404",
    "//lh5.googleusercontent.com/-4FIoLR71zJs/AAAAAAAAAAI/AAAAAAAAAAA/uio2xBeZjDw/photo.jpg",
    "https://secure.gravatar.com/avatar/c82903f2c64eecc9b9539ab780a76a9c?s=80&d=404",
    "https://lh6.googleusercontent.com/-Wx6NbaiIKQs/AAAAAAAAAAI/AAAAAAAAAAA/QIKfFUSnIEI/s0-c-k/photo.jpg"
  ],
  "emails": [
    "goofyahead@gmail.com",
    "alejandro.vidal.rodriguez@gmail.com",
    "alex@ark.com"
  ],
  "links": [
    {
      "email": "goofyahead@gmail.com",
      "network_name": "Facebook",
      "network_id": "fb",
      "profile_url": "http://www.facebook.com/alejandrovidalrodriguez",
      "profile_id": "alejandrovidalrodriguez"
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "LinkedIn",
      "network_id": "li",
      "profile_url": "http://www.linkedin.com/in/alejandrovidalrodriguez",
      "profile_id": "alejandrovidalrodriguez"
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "AngelList",
      "network_id": "ac",
      "profile_url": "http://angel.co/alejandro-vidal-rodriguez",
      "profile_id": "alejandro-vidal-rodriguez"
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "Flickr",
      "network_id": "fr",
      "profile_url": "http://www.flickr.com/photos/9269791@N02/",
      "profile_id": "9269791@N02"
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "GitHub",
      "network_id": "gh",
      "profile_url": "https://github.com/goofyahead",
      "profile_id": ""
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "Stack Overflow",
      "network_id": "so",
      "profile_url": "http://stackoverflow.com/users/758997",
      "profile_id": ""
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "Vimeo",
      "network_id": "vm",
      "profile_url": "http://vimeo.com/user11300331",
      "profile_id": "user11300331"
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "YouTube",
      "network_id": "yt",
      "profile_url": "http://youtube.com/goofyahead",
      "profile_id": "goofyahead"
    },
    {
      "email": "goofyahead@gmail.com",
      "network_name": "Google+",
      "network_id": "gp",
      "profile_url": "https://plus.google.com/114671195880788314973",
      "profile_id": "114671195880788314973"
    },
    {
      "name": "Twitter",
      "link": "https://twitter.com/undefined",
      "network_name": "Twitter",
      "profile_url": "https://twitter.com/undefined",
      "network_id": "tw",
      "profile_id": "undefined"
    }
  ],
  "education": [
    {
      "school": "Universidad Pontificia de Salamanca",
      "major": "Computer Software Engineering",
      "from": "2011",
      "to": "2012",
      "src": "li/141170624"
    }
  ],
  "languages": [
    "en",
    "es",
    "fr"
  ],
  "work": [
    {
      "company": "Nxtlink",
      "position": "Freelance developer",
      "from": "2012",
      "to": null,
      "src": "li/141170624"
    },
    {
      "company": "Telefonica I+D (R&D)",
      "position": "Mobile developer",
      "from": "2012",
      "to": "2012",
      "src": "li/141170624"
    },
    {
      "company": "ALTEN",
      "position": "Mobile development (Android, J2ME, BB) at Telefonica I+D (R&D)",
      "from": "2011",
      "to": "2012",
      "src": "li/141170624"
    },
    {
      "company": "Quadram",
      "position": "Mobile developer",
      "from": "2011",
      "to": "2011",
      "src": "li/141170624"
    },
    {
      "company": "Agnitio",
      "position": "Intern",
      "from": "2010",
      "to": "2011",
      "src": "li/141170624"
    }
  ],
  "interests": [
    
  ],
  "title": "Freelance developer"
}
```


