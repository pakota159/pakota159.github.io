---
layout: post
subtitle: Music is love, data is life 
tags: [cs, nodejs, data, spotify]
comments: true
spotify1: /img/spotify/spotify1.png
spotify2: /img/spotify/spotify2.png
spotify3: /img/spotify/spotify3.png
spotify4: /img/spotify/spotify4.png
spotify5: /img/spotify/spotify5.png
spotify6: /img/spotify/spotify6.png
---
Recently, I am working on a personal project related to analysis of music
taste of people and it requires retrieving data from some music sites like
Spotify. And fortunely, it provides some quite useful APIs that I would like
to share here.

### What I want
___
Simply I need a list of **Playlists** from Spotify including meta data of each playlist.
So, technically speaking:

My input:
- User authentication token (Spotify APIs *doesn't requires* it, but I do want to use
because it give me *higher rate limits*)
- Search key terms: ex **"Ed Sheeran"**

And I expect an output like:
- JSON data with **Playlist info**, including *metadata*
- Retrieved data should come from search results of that user identity. Ex: result is
list playlists belongs to **"Ed Sheeran"**

Okay, I now know what my goals and it's time to get things done.

### Let's start
___
Simply enough, I'll start with the [docs]('https://developer.spotify.com/documentation/web-api/quick-start/')
from official page.

We need to **create Spotify account** first that can be done easily from [https://www.spotify.com](https://www.spotify.com)

Then you need to **create developer account** to use APIs [https://developer.spotify.com/dashboard/login](https://developer.spotify.com/dashboard/login)

And last but not least, create **an app** from the dashboard [https://developer.spotify.com/dashboard/applications](https://developer.spotify.com/dashboard/applications)
to get *client id* and *client secret*

![spotify1]({{ page.spotify1 }}#post_img)

Install Nodejs because we'll need a server-side application.

Clone the repo [https://github.com/spotify/web-api-auth-examples](https://github.com/spotify/web-api-auth-examples)
that contains the authentication example app which provides a interface to register Spotify
user account to our Spotify app.

```bash
$ git clone https://github.com/spotify/web-api-auth-examples auth-app
```

Then run npm to install required packages like express,request and querystring.
```bash
$ cd auth-app
$ npm install
```

After install, we will see a new folder `node_modules` that contains all the installed modules.  
Now go into the code of this auth-app
```bash
$ cd authorization_code
```

There are 2 things inside, the `app.js` is the main code of the application, folder `public` contains
a `html` file 

Inside `app.js` there are 3 things you should care about:  
- client_id: Client Id of your app. (After create a new app as above, in the dashboard)
- client_secret: Client Secret of your app.
- redirect_uri: the url we will redirect after authenticating successfully.

The port of server is set to be `8888`, so I will set redirect_uri base on it
```javascript
var redirect_uri = 'http://localhost:8888/callback/';
```

You also need to **whitelist** your redirect_uri in the settings of your app.

![spotify3]({{ page.spotify3 }}#post_img)

Now go to `http://localhost:8888` and follow all steps to login and you should be
redirect to this after successfully login.

![spotify2]({{ page.spotify2 }}#post_img)

### Working with playlists
___
Now it's the fun part. How can I retrieve data of playlists I need.

First, copy the access token in the login page above and assign it to new
variable in `app.js`

**Note**: The access token will expire in `1 hour` so you need to refresh it,
then re-copy paste the token.

```javascript
let acc_token = <your_access_token>

// Define a new wrapper function to support GET request
let get_spotify = function (url, cb) {
	let options = {
		url: url,
		headers: {
			'Authorization': 'Bearer ' + acc_token
		},
		qs: {
			'limit': 50,
			'country': 'VN'
		},
		json: true
	};
	request.get(options, function (error, response, body) {
		cb(body);  // A callback function will handle the response
	});
}

// Define a route /get-category that call Api brose categories
app.get('/get-category', (req, res) => {
	get_spotify('https://api.spotify.com/v1/browse/categories', function(body){
		res.send({
			'data': body
		});
	})
})
```

Now go to `http://localhost:8888/get-category`, we'll get the response as
![spotify4]({{ page.spotify4 }}#post_img)

I only need **category id** to query playlists for each category. So we should
change the code a bit.
```javascript
// Define a route /get-category that call Api browse categories
app.get('/get-category', (req, res) => {
	get_spotify('https://api.spotify.com/v1/browse/categories', function(body){
		res.send({  // Using map to return only id of category
		    'data': body.categories.items.map((val)=>{return val.id})
		});
	})
})
```

and the response is an array of category ids
```json
{
  "data": [
    "toplists","vietnamese","pride","pop","kpop","mood","romance","chill","focus","party","workout","sleep","edm_dance","decades","travel","hiphop","indie_alt","popculture","gaming","karaoke","rnb","rock","dinner","roots","soul","jazz","metal","desi","country","test_latin","classical","reggae","blues","punk","funk","kids","whm"
  ]
}
```

For each category, I want to call Api once to get list of playlists I want.
The problem is nodejs is **asynchronous**, and after we make a request to query
*toplists* category, nodejs processes will continue make request to query **vietnamese**
before previous request responses. To solve that problem, we need to make sure
all the requests to all the categories *must* response completely before we response
to client.

The logic flow above can be understood as below
```bash
Make request GET /https://api.spotify.com/v1/browse/categories/toplists/playlists
to get all playlists of toplists

Make request GET /https://api.spotify.com/v1/browse/categories/vietnamese/playlists
to get all playlists of vietnamese

...
After all requests above response successfully, response to client list of
all playlists of all categories
```

To do all of these above, we'll use Promises or in this case *bluebird* package
```bash
npm install bluebird
npm install request-promise
```
Change the code to use *bluebird* and *request-promise*
```javascript
var Bluebird = require('bluebird');
var rp = require('request-promise');

app.get('/get-category', (req, res) => {
	get_spotify('https://api.spotify.com/v1/browse/categories', (options, body) => {
		// Make a list of urls and requests for playlists
		var playlist_requests = body.categories.items.map((val) => {
			options.url = 'https://api.spotify.com/v1/browse/categories/' + val.id + '/playlists'
			return rp(options)
		})
		// Call method all of Bluebird to wait all request in playlist_requests complete
		Bluebird.all(playlist_requests).then(response => {
			// When all promises/requests are completed, send results back to client
			res.send({
				'data': response.map((value) => {
					return value.playlists.items.map((val) => {
						return {
							'id': val.id,  // Return id of playlist
							'name': val.name,  // Return name of playlist
							'track': val.tracks.href,  // Return href to tracks of playlist
						}
					})
				})
			})
		})
		
		
	})
})
```

And we get result like below, with **name, id, track url** of all playlists
![spotify5]({{ page.spotify5 }}#post_img)

The track url is neccessary if we want to know **list of tracks in each playlist**

### Get all tracks in each playlist
___
Now we have playlists
```json
[
  {
    "id": "37i9dQZF1DXcBWIGoYBM5M",
    "name": "Today's Top Hits",
    "track": "https://api.spotify.com/v1/playlists/37i9dQZF1DXcBWIGoYBM5M/tracks"
  },
  {
    "id": "37i9dQZF1DX44t7uCdkV1A",
    "name": "Viral Hits",
    "track": "https://api.spotify.com/v1/playlists/37i9dQZF1DX44t7uCdkV1A/tracks"
  }
]
```

And if we make request like `GET https://api.spotify.com/v1/playlists/37i9dQZF1DX44t7uCdkV1A/tracks` we
will be able to retrieve list of songs/tracks in that playlist.

But once again, nodejs is asynchronous and there are too many playlists we need
to get tracks, we'll get Apis **limit rate error**.

How to avoid that and make more than 1000 requests now?

I don't want to directly add timeout or promises into the route function above anymore
because it would make it way too complicated function.

Thus, I decide to store all playlists I queries in a **database**, so it would make
me easier to add new playlist, check duplicated playlists, and whenever I want
to retrieve songs from a playlist, I don't have to re-call requests to playlists
apis.

I would like to use **mongodb** because it's the most familiar database to me.
You can use any of [these](https://expressjs.com/en/guide/database-integration.html)

```bash
npm install mongoose
```

Add mongoose
```javascript
var mongoose = require('mongoose');
mongoose.connect('mongodb://127.0.0.1/spotify', {useNewUrlParser: true});

const Schema = mongoose.Schema;

const PlaylistSchema = new Schema({
	playlist_name: String,
	playlist_id: String,
});

const Playlist = mongoose.model('Playlist', PlaylistSchema);

let save_playlist_to_db = function(data){
	Playlist.count({playlist_id: data.id}, function (err, count){
		if (count === 0){
			const playlist = new Playlist();
			playlist.playlist_name = data.name;
			playlist.playlist_id = data.id;
			playlist.track_href = data.track;
			playlist.save()
		}
	});
}

app.get('/get-category', (req, res) => {
	get_spotify('https://api.spotify.com/v1/browse/categories', (options, body) => {
		// Make a list of urls and requests for playlists
		var playlist_requests = body.categories.items.map((val)=>{
			var url = 'https://api.spotify.com/v1/browse/categories/' + val.id + '/playlists'
			options.url = url
			return rp(options)
		})
		// Call method all of Bluebird to wait all request in playlist_requests complete
		Bluebird.all(playlist_requests).then(response => {
			// When all promises/requests are completed, send results back to client
			res.send({
				'data': response.map((value) => {
					return value.playlists.items.map((val) => {
						var data = {
							'id': val.id,
							'name': val.name,
							'track': val.tracks.href,
						}
						save_playlist_to_db(data);
						return data
					})
				})
			})
		})	
	})
})
```

After store playlist into database, write route for query tracks, the idea
will be something such as.
```javascript
let get_playlist_from_db = function(cb){
	Playlist.find({}, function(err, playlists){
		// After query playlists from database, make promises to query songs
		
		// Make promises
		
		// Return
		return cb(playlists)
	})
}

app.get('/get-tracks', (req, res) => {
	get_playlist_from_db(function(data){
		res.send({
			'data': data
		})
	});
	
})
```

And after few changes, we have our final codes
```javascript
let get_playlist_from_db = function(cb){
    // First we query playlists from db, in this case, I limit number of 
    // results to 10 for demo
	Playlist.find({}, null, {limit: 10}, function(err, playlists){
		// A variable to store list of promises for querying tracks
		var track_requests = []
		
		// Iterate throught playlists we just queried
		playlists.forEach((val) => {
		    
		    // Push to track_request our requests
		    // something like "https://api.spotify.com/v1/playlists/37i9dQZF1DXcBWIGoYBM5M/tracks"
			track_requests.push(rp({
				uri: val.track_href,
				headers: {
					'Authorization': 'Bearer ' + acc_token
				},
				qs: {
					'limit': 100,
					'country': 'VN'
				},
				json: true
			}))
		})

		Bluebird.all(track_requests).then(response => {
			var data = []
			// When all promises/requests are completed, process the response
			response.forEach((val) => {
				val.items.forEach((value) => {
					data.push(
						{
							"playlist_id": val.href.split('/')[5],  // Extract playlist id from href
							"artists": value.track.artists,  // Artists performs this song
							"track_id": value.track.id,  // Track id
							"track_name": value.track.name,  // Track name
						}
					)
				})
			})
			
			// Return to client
			return cb(data)
		})		
	})
}

app.get('/get-tracks', (req, res) => {
	get_playlist_from_db(function(data){
		res.send({
			'data': data
		})
	});
	
})
```

And we gonna have something like this
![spotify6]({{ page.spotify6 }}#post_img)
