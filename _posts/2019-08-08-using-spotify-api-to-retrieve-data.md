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

After reading the [documents](https://developer.spotify.com/documentation/web-api/reference/playlists/)
I have a brief understand about what I can do with this api.

There are 3 ways to get info about playlists:
- Using API `/v1/users/{user_id}/playlists` to acquire playlists of a specific **user_id**
- Using API `/v1/search` to search and return playlists with a specific **query keyword**
- Using API `/v1/browse/categories/{category_id}/playlists` to retrieve playlists from
a specific **category**

I want to use the third method, because playlists I want should be distinguished by *category*
instead of user, or query keywords.

There are many categories in spotify, and each category contains many playlists, each playlist
has many tracks too. But I don't want to get all playlists from each category, just 
some most popular ones so I don't have to call too many apis.

The expected output is something like this:  
*For each category, I only need 5 most popular playlists*  
*For each playlist, I want all tracks with its name, singer, and other data*
```json
[
  {
    "category": "A",
    "playlists": [
      {
        "name": "Most popular playlist",
        "tracks": [
          {
            "track_name": "Song 1",
            "singer": "B"
          }
        ]
      }
    ]
  }
]
```

To be able to retrieve data more convenient, I would like to save category, playlists,
and tracks in database.

I'll use **mongodb** because it's the most familiar database to me.
You can use any of [these](https://expressjs.com/en/guide/database-integration.html)

First, copy the access token in the login page above and assign it to new
variable in `app.js`. And define a route `get-category` to get all categories we want.

```bash
npm install mongoose
```
 Mongoose is a mongodb object modeling tool designed to work in an asynchronous environment or
 in this case, nodejs.  
Add mongoose
```javascript
var mongoose = require('mongoose');

// Connect mongoose to our database named spotify.
mongoose.connect('mongodb://127.0.0.1/spotify', {useNewUrlParser: true});
// useNewUrlParser to fix a DeprecationWarning

// Declare schema
const Schema = mongoose.Schema;
```


### Design database
We obviously care 3 objects here: category, playlist and track, so how to design our database
to store and manipulate data easier.

There are 2 ways to design our model.  
The first one is store all 3 objects above into 1 Schema. I can call it **Category_Detail** model
The advantage is whenever I want to retrieve data from db, I only have to access one model,
no need to use embbed fields, reference.  
The disadvantage is, as I considered, bigger because I will need to store my playlists in
each model as an *array* which will really hard to update after that, and with each playlist
I need another array for tracks, so 2 nested arrays are too complicated for a model like this.

So I decide to use the second way to design my model  
3 seperated models as following *category*, *playlist* and *track*. Playlist will contains
1 reference field that refer to category, and track will contains 1 reference field refer to
playlist that it belongs to.

```javascript
const CategorySchema = new Schema({
	cat_name: String,
	cat_id: String,
});
const Category = mongoose.model('Category', CategorySchema);

const PlaylistSchema = new Schema({
	category: {type: mongoose.Schema.Types.ObjectId, ref: 'Category'},
	playlist_name: String,
	playlist_id: String,
});
const Playlist = mongoose.model('Playlist', PlaylistSchema);

const TrackSchema = new Schema({
	playlist: {type: mongoose.Schema.Types.ObjectId, ref: 'Playlist'},
	track_name: String,
	track_id: String,
	artists: Array,
	playlist_name: String,
	playlist_id: String,
});
const Track = mongoose.model('Track', TrackSchema);
```

### Get category
___
Now, we can define a new route to get category
```javascript
app.get('/get-category', (req, res) => {
	var options = {
		url: 'https://api.spotify.com/v1/browse/categories',
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
		res.send({
			'data': body
		})
	});
})
```
Now go to `http://localhost:8888/get-category`, we'll get the response as
![spotify4]({{ page.spotify4 }}#post_img)

I only need **category id** to query playlists for each category. So we should
change the code a bit.
```javascript
// Define a function that store category
let save_category_to_db = function(data){
	Category.count({cat_id: data.id}, function (err, count){
		if (count === 0){
			const cat = new Category();
			cat.cat_id = data.id;
			cat.cat_name = data.name;
			cat.save()
		}
	});
}
// Define a route /get-category that call Api browse categories
app.get('/get-category', (req, res) => {
	var options = {
		url: 'https://api.spotify.com/v1/browse/categories',
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
		// Store category to db
		body.categories.items.forEach((val) => {
			save_category_to_db(val)
		})
		// Response
		res.send({
			'data': 'Success'
		})
	});
})
```

and in db, we have our categories
```json
[
    { 
        "_id" : "5d52b6f2de0da87f6ec98e7f", 
        "cat_id" : "toplists", 
        "cat_name" : "Top Lists"
    },
    { 
        "_id" : "5d52b6f2de0da87f6ec98e80", 
        "cat_id" : "pride", 
        "cat_name" : "Pride"
    },
    { 
        "_id" : "5d52b6f2de0da87f6ec98e82", 
        "cat_id" : "kpop", 
        "cat_name" : "K-Pop" 
    }
]
```
### Get playlist
___
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

Make request GET /https://api.spotify.com/v1/browse/categories/kpop/playlists
to get all playlists of kpop

...
After all requests above response successfully, save those playlists to db
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

let save_playlist_to_db = function(data){
	var cat_id = data.href.split('/')[6]  // Extract cat id from href in response
	Category.findOne({cat_id: cat_id}, function(err, doc){
		if(doc){
			data.items.forEach(val => {
				Playlist.count({playlist_id: val.id}, function (err, count){
					if (count === 0){
						const playlist = new Playlist();
						playlist.playlist_name = val.name;
						playlist.playlist_id = val.id;
						playlist.category = doc;
						playlist.save()
					}
				});
			})
		}
	})
}

app.get('/get-playlist', (req, res) => {
	// Get all categories in db
	Category.find({}, function(err, playlists){
		var playlist_requests = playlists.map((val) => {
			// For each category, make promise
			return rp({
				url: 'https://api.spotify.com/v1/browse/categories/' + val.cat_id + '/playlists',
				headers: {
					'Authorization': 'Bearer ' + acc_token
				},
				qs: {
					'limit': 50,
					'country': 'VN'
				},
				json: true
			})
		})

		Bluebird.all(playlist_requests).then(response => {
			// After response completed, store playlist in db
			response.map((value) => {
				save_playlist_to_db(value.playlists)
			})
			res.send({
				'data': response
			})
		})
	})
})
```

And we get result like below, with **name, id, track url** of all playlists
```json
[
    { 
        "_id" : "5d52bf2aae62ab8263811977", 
        "playlist_name" : "Viral Hits", 
        "playlist_id" : "37i9dQZF1DX44t7uCdkV1A", 
        "category" : "5d52b6f2de0da87f6ec98e7f"
    },
    { 
        "_id" : "5d52bf2aae62ab8263811978", 
        "playlist_name" : "Viral 50 Việt Nam", 
        "playlist_id" : "37i9dQZEVXbL1G1MbPav3j", 
        "category" : "5d52b6f2de0da87f6ec98e7f" 
    },
    { 
        "_id" : "5d52bf2aae62ab826381197c",
        "playlist_name" : "New Music Friday Malaysia", 
        "playlist_id" : "37i9dQZF1DWZMWLrh2UzwC", 
        "category" : "5d52b6f2de0da87f6ec98e7f"
    }
]
```

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

So we need to make seperated requests to avoid the error above. I make new route
```javascript
app.get('/get-tracks', (req, res) => {
	get_tracks(function(response){
	    // get_tracks function will receive 1 callback to response to client
		res.send({
			'data': response
		})
	});	
})

```
The function `get_tracks` will do something for us:
- Query all category from database
- From each category, take 2 or 3 playlists
- From each playlist, call api GET tracks from playlist

```javascript
let get_tracks = function(cb){
	Category.find({}, function(err, cats){
		var promise_arr = [];
		var query_promises = [];
		cats.forEach(cat => {
			query_promises.push(
				Playlist.find({category: cat.id}, null, {limit: 3}).exec()
			)
		})
		
		// This promise is query promise to make sure we call api after completing all queries
		Promise.all(query_promises).then(results => {
			results.forEach(playlists => {
				// For each playlist, make promise
				playlists.forEach(val => {
					promise_arr.push(
						rp({
							url: 'https://api.spotify.com/v1/playlists/' + val.playlist_id + '/tracks',
							headers: {
								'Authorization': 'Bearer ' + acc_token
							},
							qs: {
								'limit': 100,
								'country': 'VN'
							},
							json: true
						})
					)
				})
			})

			Bluebird.all(promise_arr).then(response => {
				response.forEach(val => {
				    // After finishing calling API, save response data to database
					save_track_to_db(val)
				})
			}).catch(err => {
				console.log(err)
			})
			
			// Because query and saving data took too much time, I response to client this msg
			cb('query processing')
		})
	})
}
```

After calling API completely, we save the response data to track database
```javascript
let save_track_to_db = function(data){
	var playlist_id = data.href.split('/')[5]
	Playlist.findOne({playlist_id: playlist_id}, function(err, pl){
		console.log(data.items[0].track)
		data.items.forEach(val => {
			if(val && val.track){
				Track.count({track_id: val.track.id, playlist: pl}, function(err, count){
					if(count === 0){
						const track = new Track();
						track.track_id = val.track.id;
						track.track_name = val.track.name;
						track.playlist = pl;
						track.artists = val.track.artists;
						track.playlist_name = pl.playlist_name;
						track.playlist_id = pl.playlist_id;
						track.save()
						console.log('Done save track ' + val.track.name)
					}
				})
			}
			
		})
	})
}
```

As a result now we have track database like this
```json
 [
     {
        "_id": "5d538fca355eb39108dc0ed1", 
        "artists" : [
            {
                "external_urls" : {
                    "spotify" : "https://open.spotify.com/artist/0r63ReVRjxrS4ATbLrdcrL"
                }, 
                "href" : "https://api.spotify.com/v1/artists/0r63ReVRjxrS4ATbLrdcrL", 
                "id" : "0r63ReVRjxrS4ATbLrdcrL", 
                "name" : "Hoang Thuy Linh", 
                "type" : "artist", 
                "uri" : "spotify:artist:0r63ReVRjxrS4ATbLrdcrL"
            }
        ], 
        "track_id" : "4V1BqUA97pWQpPB3gxWwoQ", 
        "track_name" : "De Mi Noi Cho Ma Nghe", 
        "playlist_name" : "Viral 50 Việt Nam", 
        "playlist_id" : "37i9dQZEVXbL1G1MbPav3j"
    },
    { 
        "_id" : "5d538fca355eb39108dc0ed2", 
        "artists" : [
            {
                "external_urls" : {
                    "spotify" : "https://open.spotify.com/artist/1K8kkeM8j0BL8sQ4aR7Vh6"
                }, 
                "href" : "https://api.spotify.com/v1/artists/1K8kkeM8j0BL8sQ4aR7Vh6", 
                "id" : "1K8kkeM8j0BL8sQ4aR7Vh6", 
                "name" : "HYOMIN", 
                "type" : "artist", 
                "uri" : "spotify:artist:1K8kkeM8j0BL8sQ4aR7Vh6"
            }, 
            {
                "external_urls" : {
                    "spotify" : "https://open.spotify.com/artist/3rjcQ5VIWCN4q7UFetzdeO"
                }, 
                "href" : "https://api.spotify.com/v1/artists/3rjcQ5VIWCN4q7UFetzdeO", 
                "id" : "3rjcQ5VIWCN4q7UFetzdeO", 
                "name" : "JustaTee", 
                "type" : "artist", 
                "uri" : "spotify:artist:3rjcQ5VIWCN4q7UFetzdeO"
            }
        ], 
        "track_id" : "1YX290GRxBTdJ7C0rJBzF0", 
        "track_name" : "Cabinet", 
        "playlist_name" : "Viral 50 Việt Nam", 
        "playlist_id" : "37i9dQZEVXbL1G1MbPav3j"
    }
]
```