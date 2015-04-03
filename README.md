Staance Coding Challenge v1.0

Introduction:

	Your mission, should you choose to accept it, is to implement the view for a Staance Feed.  
	A feed is a collection of assertions that are related to each other generally by a “tag” or a “category”; 
	for this exercise you will be focusing on the “Gaming” Feed. You can view the current version of the 
	Gaming feed at http://staance.com/gaming in order to get a sense of what a feed consist of.  
	
	Good Luck and Have Fun!

Requirements: 

Your design must have the following features:
The feed must scroll horizontally
You must show image, video, iframe, brief, link if any of these are available
You must be able to Agree or Disagree with an assertion
Then the opinions for that assertion should be displayed
Construct a pie chart for each assertion
The data should be represented as a fixed position bar at the bottom which breaks down the agree / disagree stats when clicked on.
Should be 100% width and 100px height
Should include one pie chart for each assertion
And each pie should include the agree / disagree break down.
In the image below you can see the icons to click to display the pie charts:


You are free to use any libraries that you may need (the choice is yours, but expect to defend your decisions).  Also, please push your code to: 

https://github.com/dpow101/codeChallenge.git

And please feel free to reach out if you have any questions or comments.

Background Information:
API:

	You can access the API endpoints at http://10.0.1.2:3005. For this exercise you will need access to these endpoints:
GET: /v1.3.1/feed/gaming
POST: /v1.3.1/assertion/{assertion_id}/{staance: (agree/disagree)}
GET: /v1.3.1/assertion/{assertion_id}/opinions

Access to these endpoints require an authentication.  Authentication is verified via a token in the headers as ‘x-auth-token’..  For training purposes you may use this token for all your request: 

519a42825b56a06706c1d8286468c78400e3497c781f6e2247fc5cd9c328d8b30ad90259a119a0f45dc512313aca07eb41906ce66f2c78731437dd8e3ecf46432dc68ce46644b56b18e3013fe48bc50f2cfa1ae93ce878f0bf9cfc42e9d072e1

Feeds Endpoint:
	The feeds endpoint uses query parameters: limit, offset, and window_token. You may use window_token if you wish, but it is not required. A window token is a session string that removes seen assertions from a feed (mainly used on iOS) and can expire. A sample JSON payload of a feed looks as follows: 
Sample JSON Response

GET  http://10.0.1.2:3005/v1.3.1/feed/gaming?limit=1&offset=0

{
    "meta": {
        "limit": 1,
        "offset": 0,
        "next_offset": 1,
        "fid": "f/gaming",
        "type": "feeds",
        "window_token": "{\"keys\":\"16105\",\"session_date\":1428086813780}",
        "request_url": "/v1.3.1/feed/gaming?limit=1&offset=0",
        "request_time_ms": 1
    },
    "feeds": [
        {
            "fid": "f/gaming",
            "title": "Gaming",
            "score": 10,
            "assertions": [
                {
                    "aid": "a16105",
                    "title": "Dice is losing it.",
                    "slab_text": "Dice is\nlosing\nit",
                    "type": [
                        "topic"
                    ],
                    "media": [],
                    "event": [],
                    "quote": {},
                    "feeds": [
                        "f/popular",
                        "f/today",
                        "f/gaming",
                        "t/ea",
                        "t/dice",
                        "t/influencer",
                        "t/david-powell",
                        "t/february4"
                    ],
                    "tags": [
                        "ea",
                        "dice",
                        "influencer",
                        "david-powell",
                        "february4"
                    ],
                    "created": "2015-02-04T22:56:27.553Z",
                    "expired": "2015-02-18T22:56:27.553Z",
                    "status": "A",
                    "score": 1423090587553,
                    "creator": {
                        "uid": "u18389",
                        "username": "David Powell",
                        "display_name": "David Powell",
                        "is_contributor": true,
                        "is_guest": false,
                        "profile_url": "http://media.staance.com/user/photo/18389"
                    },
                    "stat_agrees": 0,
                    "stat_disagrees": 0,
                    "stat_agrees_male": 0,
                    "stat_disagrees_male": 0,
                    "stat_agrees_female": 0,
                    "stat_disagrees_female": 0
                }
            ]
        }
    ]
}
Assertion Agree/Disagree Endpoint:
	The agree/disagree endpoint (also referred to as the staancing endpoint) is a POST and only requires an assertion ID in the url. The server will not allow you to staance an assertion multiple times and will return the assertion in the response JSON payload. Here is a sample JSON response:

Sample JSON Response

POST http://10.0.1.2:3005/v1.3.1/assertion/a16105/agree

{
    "meta": {
        "type": "assertions",
        "stance": "agree",
        "request_url": "/v1.3.1/assertion/a16105/agree",
        "request_time_ms": 14
    },
    "assertions": [
        {
            "aid": "a16105",
            "title": "Dice is losing it.",
            "slab_text": "Dice is\nlosing\nit",
            "type": [
                "topic"
            ],
            "media": [],
            "event": [],
            "quote": {},
            "feeds": [
                "f/popular",
                "f/today",
                "f/gaming",
                "t/ea",
                "t/dice",
                "t/influencer",
                "t/david-powell",
                "t/february4"
            ],
            "tags": [
                "ea",
                "dice",
                "influencer",
                "david-powell",
                "february4"
            ],
            "created": "2015-02-04T22:56:27.553Z",
            "expired": "2015-02-18T22:56:27.553Z",
            "status": "A",
            "score": 1423090587553,
            "creator": {
                "uid": "u18389",
                "username": "David Powell",
                "display_name": "David Powell",
                "is_contributor": true,
                "is_guest": false,
                "profile_url": "http://media.staance.com/user/photo/18389"
            },
            "stat_agrees": 1,
            "stat_disagrees": 0,
            "stat_agrees_male": 0,
            "stat_disagrees_male": 0,
            "stat_agrees_female": 0,
            "stat_disagrees_female": 0
        }
    ]
}
Opinions Endpoint:
	The Opinions Endpoint requires an assertion id and will return an array of opinion objects.
Sample JSON Response

GET http://10.0.1.2:3005/v1.3.1/assertion/a11111/opinions

{
    "meta": {
        "type": "opinions",
        "request_url": "/v1.3.1/assertion/a11111/opinions",
        "request_time_ms": 9
    },
    "opinions": [
        {
            "aid": "a11111",
            "oid": "o11668",
            "creator": {
                "uid": "u10004",
                "username": "Jimmy S.",
                "display_name": "Jimmy S.",
                "is_contributor": false,
                "is_guest": false,
                "profile_url": "http://media.staance.com/user/photo/10004"
            },
            "text": "He's obviously lost the team and I don't see how they can start winning with him. Something needs to change, and players should be included.",
            "created": "2013-12-09T15:23:45.831Z",
            "assertion_stance": 1,
            "type": "opinion",
            "comment_count": 0,
            "stance": 0,
            "stat_agrees": 1,
            "stat_disagrees": 0
        },...
    ]
}

