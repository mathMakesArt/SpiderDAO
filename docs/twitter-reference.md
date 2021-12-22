# **Twitter Reference**

TODO:
  1. Finish the intro table by filling out the "OPTIONAL INPUTS" column for each type of API call

## **VARIABLE REFERENCE TABLE**

| **NAME OF API CALL**        | **LIMITING VARIABLE**         | **URL ENDPOINT STRING**         | **REQUIRED IN**  | **OPTIONAL INPUTS**                      |
| --------------------------- | ----------------------------- | ------------------------------- | ---------------- | ---------------------------------------- |
| USER_VIA_USERNAME           | 12: RL_USER_LOOKUP            | 2/users/by/username/:username   | username         | expansions, tweet.fields, user.fields    |
| USERS_VIA_USERNAME          | 12: RL_USER_LOOKUP            | 2/users/by                      | usernameList     | expansions, tweet.fields, user.fields    |
| USER_VIA_USERID             | 12: RL_USER_LOOKUP            | 2/users/:id                     | id (User)        | expansions, tweet.fields, user.fields    |
| USERS_VIA_USERIDS           | 12: RL_USER_LOOKUP            | 2/users                         | idList (User)    | expansions, tweet.fields, user.fields    |
| LISTS_VIA_MEMBER_USERID     | 18: RL_LISTS_VIA_MEMBER       | 2/users/:id/list_memberships    | id (User)        | PLACEHOLDER    |
| LISTS_VIA_OWNER_USERID      | 15: RL_LISTS_VIA_OWNER        | 2/users/:id/owned_lists         | id (User)        | PLACEHOLDER    |
| LISTS_VIA_FOLLOWER_USERID   | 20: RL_LISTS_VIA_FOLLOWER     | 2/users/:id/followed_lists      | id (User)        | PLACEHOLDER    |
| LISTS_VIA_PINNER_USERID     | 21: RL_LISTS_VIA_PINNER       | 2/users/:id/pinned_lists        | id (User)        | PLACEHOLDER    |
| LIST_VIA_LISTID             | 14: RL_LIST_LOOKUP            | 2/lists/:id                     | id (List)        | PLACEHOLDER    |
| MEMBERS_VIA_LISTID          | 17: RL_MEMBERS_VIA_LIST       | 2/lists/:id/members             | id (List)        | PLACEHOLDER    |
| FOLLOWERS_VIA_LISTID        | 19: RL_FOLLOWERS_VIA_LIST     | 2/lists/:id/followers           | id (List)        | PLACEHOLDER    |
| FOLLOWERS_VIA_USERID        | 13: RL_FOLLOWS_VIA_USER       | 2/users/:id/followers           | id (User)        | PLACEHOLDER    |
| FRIENDS_VIA_USERID          | 13: RL_FOLLOWS_VIA_USER       | 2/users/:id/following           | id (User)        | PLACEHOLDER    |
| TWEETS_VIA_USERID           | 01: RL_TWEETS_VIA_USER        | 2/users/:id/tweets              | id (User)        | PLACEHOLDER    |
| MENTIONS_VIA_USERID         | 02: RL_MENTIONS_VIA_USER      | 2/users/:id/mentions            | id (User)        | PLACEHOLDER    |
| LIKES_VIA_USERID            | 10: RL_LIKES_VIA_USER         | 2/users/:id/liked_tweets        | id (User)        | PLACEHOLDER    |
| LIKES_VIA_TWEETID           | 11: RL_LIKES_VIA_TWEET        | 2/tweets/:id/liking_users       | id (Tweet)       | PLACEHOLDER    |
| RETWEETS_VIA_TWEETID        | 09: RL_RETWEETS_VIA_TWEET     | 2/tweets/:id/retweeted_by       | id (Tweet)       | PLACEHOLDER    |
| TWEET_VIA_TWEETID           | 00: RL_TWEET_LOOKUP           | 2/tweets/:id                    | id (Tweet)       | PLACEHOLDER    |
| TWEETS_VIA_TWEETIDS         | 00: RL_TWEET_LOOKUP           | 2/tweets                        | idList (Tweet)   | PLACEHOLDER    |
| TWEETS_VIA_SEARCH_RECENT    | 03: RL_TWEETS_SEARCH_RECENT   | 2/tweets/search/recent          | query            | PLACEHOLDER    |
| COUNTS_VIA_SEARCH_RECENT    | 05: RL_COUNTS_SEARCH_RECENT   | 2/tweets/counts/recent          | query            | PLACEHOLDER    |
| TWEETS_VIA_LISTID           | 16: RL_LIST_TWEETS            | 2/lists/:id/tweets              | id (List)        | PLACEHOLDER    |

<br />
<br />

## **TWITTER API USAGE GUIDELINES**

1. Unless otherwise specified, the following rules will apply
  1. API queries will take at most a single input value.
    1. In cases where multiple input values are provided, should maximize the inputs per requests wherever possible
  2. API queries will return multiple output values
  3. API queries do not require a pagination input value
  4. Multi-return API queries return the maximum possible count by default
  5. Multi-return API queries are unbounded (beyond single-page-per-return limits)
  6. Unbounded multi-return API queries accept a pagination_token input variable (the page number to load)

2. EXCEPTIONS to the above rules:
    1. The queries which support multiple simultaneous inputs are:
        1.    `GET /2/users/by`
              (1-100 simultaneous inputs, as Twitter usernames)
        2.   `GET /2/users`
                (1-100 simultaneous inputs, as Twitter Account IDs)
        3.  `GET /2/tweets`
                (1-100 simultaneous inputs, as Tweet IDs)

    2. The queries which support only a single return per request are:
        1.    `GET /2/tweets/:id`
              (Returns the details of a single Tweet, specified by Tweet ID)
        2.   `GET /2/users/:id`
              (Returns the details of a single User, specified by User ID)
        3.  `GET /2/lists/:id`
              (Returns the details of a single List, specified by List ID)

    3. The queries which require a pagination input value are:
        1.    `GET /2/users/:id/liked_tweets`
              (100 Tweet results per page)
        2.   `GET /2/users/:id/following`
              (1,000 User results per page)
        3.  `GET /2/users/:id/followers`
              (1,000 User results per page)
        4.   `GET /2/lists/:id/members`
              (100 User results per page)
        5.    `GET /2/lists/:id/followers`
              (100 User results per page)
        6.   `GET /2/users/:id/owned_lists`
              (100 User results per page)
        7.  `GET /2/users/:id/list_memberships`
              (100 Tweet results per page)
        8. `GET /2/users/:id/followed_lists`
              (100 Tweet results per page)
        9.   `GET /2/users/:id/tweets`
              (100 Tweet results per page)
        10.    `GET /2/users/:id/mentions`
              (100 Tweet results per page)

    4. The queries which require manual specification of the maximum return count are:
        1.    `GET /2/users/:id/following`
              (1000 is maximum; 100 is default)
        2.   `GET /2/users/:id/followers`
              (1000 is maximum; 100 is default)
        3.  `GET /2/users/:id/tweets`
              (100 is maximum; 10 is default)
        4.   `GET /2/users/:id/mentions`
              (100 is maximum; 10 is default)

    5. The exception queries which are bounded in some form are:
        1.    `GET /2/tweets/:id/liking_users`
              (Returns only 100 Users at most, specifically most recent retweet-ers)
        2.   `GET /2/tweets/:id/retweeted_by`
              (Returns only 100 Users at most, specifically most recent retweet-ers)
        3.  `GET /2/users/:id/tweets`
              (Returns only 3200 most recent Tweets by user; maximum 100 per page)
        4.   `GET /2/users/:id/mentions`
              (Returns only 800 most recent Tweets mentioning user; maximum 100 per page)

    6. The unbounded multi-return queries which do not accept a "pagination_token" input are:
        1.    `GET /2/tweets/search/recent`
              (Must advance using the "next_token" value, one page at a time, via consecutive calls)

<br />
<br />

## **RATE LIMITS (REQUESTS PER EPOCH) REFERENCE**

Order of ratelimit variables below comes from official Twitter API v2 Rate Limits documentation:

https://developer.twitter.com/en/docs/twitter-api/rate-limits

<br />

0.   Tweet(s) via Tweet ID(s). (Can include any further context from tweet.fields)

     `RL_TWEET_LOOKUP = 900`

1.   Recent Tweets (including RTs and QTs) by a User, via User ID

     `RL_TWEETS_VIA_USER = 1500`

2.   Recent Mentions of a User (by other accounts), via User ID

     `RL_MENTIONS_VIA_USER = 450`

3.   Search endpoint for recent Tweets, via a query (e.g. keyword)

     `RL_TWEETS_SEARCH_RECENT = 450`

4.   (NOT YET IMPLEMENTED) Search endpoint for FULL ARCHIVE Tweets, via a query (e.g. keyword) (NOT YET IMPLEMENTED)

     `RL_SEARCH_TWEETS_FULL = 300`  Academic endpoints are not yet supported!

5.   "Tweet Counts" endpoint for recent Tweets, via a query (e.g. keyword)

     `RL_COUNTS_SEARCH_RECENT = 300`

6.   (NOT YET IMPLEMENTED) "Tweet Counts" endpoint for FULL ARCHIVE Tweets, via a query (e.g. keyword) (NOT YET IMPLEMENTED)

     `RL_TWEET_COUNTS_FULL = 300`   Academic endpoints are not yet supported!

7.   (NOT YET IMPLEMENTED) Initiating connections to a Filtered Stream (NOT YET IMPLEMENTED)

     `RL_STREAMS_CONNECTING = 50`

8.   (NOT YET IMPLEMENTED) Listing filters for a (connected) Filtered Stream (NOT YET IMPLEMENTED)

     `RL_STREAMS_LISTING = 450`

9.   Up to 100 of the most recent Users to RETWEET a given Tweet, via Tweet ID

     `RL_RETWEETS_VIA_TWEET = 75`

10.  Tweets recently Liked by a given account, via User ID

     `RL_LIKES_VIA_USER = 75`

11.  Up to 100 of the most recent Users to LIKE a given Tweet, via Tweet ID

     `RL_LIKES_VIA_TWEET = 75`

12.  User lookup, traditionally via User ID but also by Username. (Can include any further context from user.fields, and tweet.fields for PINNED TWEET)

     `RL_USER_LOOKUP = 900`

13.  Can return Followers and Friends (following) of a given User, via User ID

     `RL_FOLLOWS_VIA_USER = 15`

14.  List lookup for a single List, via List ID. (Can include any further context from list.fields, and user.fields for LIST OWNERS)

     `RL_LIST_LOOKUP = 75`

15.  Returns Lists OWNED by a given User, via User ID

     `RL_LISTS_VIA_OWNER = 75`

16.  Endpoint for viewing recent tweets from a given single List, via List ID

     `RL_LIST_TWEETS = 900`  "LIST TWEETS" refers to "Tweets from (a) List", not "(a) list of Tweets"

17.  Returns Users who are MEMBERS of a given List, via List ID

     `RL_MEMBERS_VIA_LIST = 900`

18.  Returns Lists in which a given User has MEMBERSHIP, via User ID

     `RL_LISTS_VIA_MEMBER = 75`

19.  Returns Users who FOLLOW a given List, via List ID

     `RL_FOLLOWERS_VIA_LIST = 180`

20.  Returns Lists for which a given User is a FOLLOWER, via User ID

     `RL_LISTS_VIA_FOLLOWER = 15`

21.  Returns Lists which a given User has PINNED, via User ID

     `RL_LISTS_VIA_PINNER = 15`

22.  (NOT YET IMPLEMENTED) "Spaces Lookup" endpoint (NOT YET IMPLEMENTED)

     `RL_SPACES_LOOKUP = 300`

23.  (NOT YET IMPLEMENTED) "Search Spaces" endpoint (NOT YET IMPLEMENTED)

     `RL_SEARCH_SPACES = 300`

<br />
<br />

## **Twitter API v2 ENDPOINTS REFERENCE**

### **BY USERNAME**

### *GET /2/users/by/username/:username*
* Returns a variety of information about a single user, specified by username.
* https://developer.twitter.com/en/docs/twitter-api/users/lookup/api-reference/get-users-by-username-username
* Endpoint URL
    * https://api.twitter.com/2/users/by/username/:username
* Limitations
    * 900 requests per period (12: RL_USER_LOOKUP)
* Input
    * Twitter account username
* Output
    * User ID of given account

### *GET /2/users/by*
* Returns a variety of information about one or more users specified by their usernames.
* https://developer.twitter.com/en/docs/twitter-api/users/lookup/api-reference/get-users-by
* Endpoint URL
    * https://api.twitter.com/2/users/by
* Limitations
    * 900 requests per period (12: RL_USER_LOOKUP)
    * 100 maximum input users (output size is defined by number of input IDs)
* Input
    * Twitter account username(s), up to 100 (?usernames="user1,user2,user3")
* Output
    * User ID(s) of given account(s)

<br />
<br />

### **BY USER ID** (Part 2: Follows, Tweets by, Mentions of, Likes by)

### *GET /2/users/:id*
* Returns a variety of information about a single user specified by the requested ID.
* https://developer.twitter.com/en/docs/twitter-api/users/lookup/api-reference/get-users-id
* Endpoint URL
    * https://api.twitter.com/2/users/:id
* Limitations
    * 900 requests per period (12: RL_USER_LOOKUP)
* Input
    * User ID (SINGLE INPUT)
* Output
    * User information for the provided ID

<br />
<br />

### **USERS BY USER IDs (PLURAL)**

### *GET /2/users*
* Returns a variety of information about one or more users specified by the requested IDs.
* https://developer.twitter.com/en/docs/twitter-api/users/lookup/api-reference/get-users
* Endpoint URL
    * https://api.twitter.com/2/users
* Limitations
    * 900 requests per period (12: RL_USER_LOOKUP)
    * 100 maximum input users (output size is defined by number of input IDs)
* Input
    * User ID(s), up to 100
* Output
    * User information for each provided ID

### *GET /2/users/:id/list_memberships*
* Returns all Lists in which a single specified user is a member
* https://developer.twitter.com/en/docs/twitter-api/lists/list-members/api-reference/get-users-id-list_memberships
* Endpoint URL
    * https://api.twitter.com/2/users/:id/list_memberships
* Limitations
    * 75 requests per period (18: RL_LISTS_VIA_MEMBER)
    * 100 results per page (max_results: default 100, already maximum)
* Input
    * User ID (SINGLE INPUT)
    * pagination_token
* Output
    * Lists of which user is a member (up to 100 List IDs)

### *GET /2/users/:id/owned_lists*
* Returns all Lists owned by the specified user.
* https://developer.twitter.com/en/docs/twitter-api/lists/list-lookup/api-reference/get-users-id-owned_lists
* Endpoint URL
    * https://api.twitter.com/2/users/:id/owned_lists
* Limitations
    * 15 requests per period (15: RL_LISTS_VIA_OWNER)
    * 100 results per page (max_results: default 100, already maximum)
* Input
    * User ID (SINGLE INPUT)
    * pagination_token
* Output
    * List(s) owned by user (up to 100 List IDs)

### *GET /2/users/:id/followed_lists*
* Returns all Lists followed by a single specified user
* https://developer.twitter.com/en/docs/twitter-api/lists/list-follows/api-reference/get-users-id-followed_lists
* Endpoint URL
    * https://api.twitter.com/2/users/:id/followed_lists
* Limitations
    * 15 requests per period (20: RL_LISTS_VIA_FOLLOWER)
    * 100 results per page (max_results: default 100, already maximum)
* Input
    * User ID (SINGLE INPUT)
    * pagination_token
* Output
    * Lists followed by User (up to 100 List IDs)

### *GET /2/users/:id/pinned_lists*
* Returns all Lists pinned by a single specified user
* https://developer.twitter.com/en/docs/twitter-api/lists/pinned-lists/api-reference/get-users-id-pinned_lists
* Endpoint URL
    * https://api.twitter.com/2/users/:id/pinned_lists
* Limitations
    * 15 requests per period (21: RL_LIST_VIA_PINNER)
* Input
    * User ID (SINGLE INPUT)
* Output
    * Lists pinned by User

<br />
<br />

### **BY LIST ID**

### *GET /2/lists/:id*
* Returns the details of a specified List.
* https://developer.twitter.com/en/docs/twitter-api/lists/list-lookup/api-reference/get-lists-id
* Endpoint URL
    * https://api.twitter.com/2/lists/:id
* Limitations
    * 75 requests per period (14: RL_LIST_LOOKUP)
* Input
    * List ID (SINGLE INPUT)
* Output
    * Details of the given list

### *GET /2/lists/:id/members*
* Returns a list of users who are members of the specified List.
* https://developer.twitter.com/en/docs/twitter-api/lists/list-members/api-reference/get-lists-id-members
* Endpoint URL
    * https://api.twitter.com/2/lists/:id/members
* Limitations
    * 900 requests per period (17: RL_MEMBERS_VIA_LIST)
    * 100 results per page (max_results: default 100, already maximum)
* Input
    * List ID (SINGLE INPUT)
    * pagination_token
* Output
    * Users with membership in List (up to 100 User IDs)

### *GET /2/lists/:id/followers*
* Returns a list of users who are followers of the specified List.
* https://developer.twitter.com/en/docs/twitter-api/lists/list-follows/api-reference/get-lists-id-followers
* Endpoint URL
    * https://api.twitter.com/2/lists/:id/followers
* Limitations
    * 180 requests per period (19: RL_FOLLOWERS_VIA_LIST)
    * 100 results per page (max_results: default 100, already maximum)
* Input
    * List ID (SINGLE INPUT)
    * pagination_token
* Output
    * Users who follow the List (up to 100 User IDs)

<br />
<br />

### **BY USER ID** (Part 2: Follows, Tweets by, Mentions of, Likes by)

### *GET /2/users/:id/followers*
* Returns a list of users who are followers of the specified user ID.
* https://developer.twitter.com/en/docs/twitter-api/users/follows/api-reference/get-users-id-followers
* Endpoint URL
    * https://api.twitter.com/2/users/:id/followers
* Limitations
    * 15 requests per period (13: RL_FOLLOWS_VIA_USER)
    * 1000 results per page (max_results: default 100, maximum of 1000)
* Input
    * User ID (SINGLE INPUT)
    * max_results (1000 for maximum)
    * pagination_token
* Output
    * List of users who are following the given User ID

### *GET /2/users/:id/following*
* Returns a list of "friends" (users followed by the specified user ID)
* https://developer.twitter.com/en/docs/twitter-api/users/follows/api-reference/get-users-id-following
* Endpoint URL
    * https://api.twitter.com/2/users/:id/following
* Limitations
    * 15 requests per period (13: RL_FOLLOWS_VIA_USER)
    * 1000 results per page (max_results: default 100, maximum of 1000)
* Input
    * User ID (SINGLE INPUT)
    * max_results (1000 for maximum)
    * pagination_token
* Output
    * List of users who are friends of (followed by) the given User ID

### *GET /2/users/:id/tweets*
* Returns up to 3200 of the most recent Tweets BY a user (100 per page)
* https://developer.twitter.com/en/docs/twitter-api/tweets/timelines/api-reference/get-users-id-tweets
* Endpoint URL
    * https://api.twitter.com/2/users/:id/tweets
* Limitations
    * 1500 requests per period (1: RL_TWEETS_VIA_USER)
    * 100 results per page (max_results: 100 is maximum, 10 is default)
* Input
    * User ID (SINGLE INPUT)
    * max_results (100 for maximum)
    * pagination_token
* Output
    * Tweet IDs of tweets BY the provided account

### *GET /2/users/:id/mentions*
* Returns up to 800 of the most recent Tweets MENTIONING a user (100 per page)
* https://developer.twitter.com/en/docs/twitter-api/tweets/timelines/api-reference/get-users-id-mentions
* Endpoint URL
    * https://api.twitter.com/2/users/:id/mentions
* Limitations
    * 450 requests per period (2: RL_MENTIONS_VIA_USER)
    * 100 results per page (max_results: 100 is maximum, 10 is default)
* Input
    * User ID (SINGLE INPUT)
    * max_results (100 for maximum)
    * pagination_token
* Output
    * Tweet IDs of tweets MENTIONING the provided account

### *GET /2/users/:id/liked_tweets*
* Allows you to get information about a user’s liked Tweets.
* https://developer.twitter.com/en/docs/twitter-api/tweets/likes/api-reference/get-users-id-liked_tweets
* Endpoint URL
    * https://api.twitter.com/2/users/:id/liked_tweets
* Limitations
    * 75 requests per period (10: RL_LIKES_VIA_USER)
    * 100 results per page (max_results: default 100, already maximum)
* Input
    * User ID (SINGLE INPUT)
    * pagination_token
* Output
    * Tweet IDs of liked tweets (paginated with 100 per page)

<br />
<br />

### **BY TWEET ID**

### *GET /2/tweets/:id/liking_users*
* Allows you to get information about a Tweet’s liking users.
* https://developer.twitter.com/en/docs/twitter-api/tweets/likes/api-reference/get-tweets-id-liking_users
* Endpoint URL
    * https://api.twitter.com/2/tweets/:id/liking_users
* Limitations
    * 75 requests per period (11: RL_LIKES_VIA_TWEET)
    * Maximum of 100 liking users returned by request (no way to change)
* Input
    * Tweet ID (SINGLE INPUT)
* Output
    * User IDs of liking users (up to 100 most recent)

### *GET /2/tweets/:id/retweeted_by*
* Allows you to get information about who has Retweeted a Tweet.
* https://developer.twitter.com/en/docs/twitter-api/tweets/retweets/api-reference/get-tweets-id-retweeted_by
* Endpoint URL
    * https://api.twitter.com/2/tweets/:id/retweeted_by
* Limitations
    * 75 requests per period (9: RL_RETWEETS_VIA_TWEET)
    * 100 total results per request (most recent 100 only; no way to return more)
* Input
    * Tweet ID (SINGLE INPUT)
* Output
    * User IDs of retweeting users (most recent, up to maximum of 100 retweets)

<br />
<br />

### **TWEETS BY TWEET ID (SINGLE)**

### *GET /2/tweets/:id*
* Returns a variety of information about a single Tweet specified by the requested ID.
* https://developer.twitter.com/en/docs/twitter-api/tweets/lookup/api-reference/get-tweets-id
* Endpoint URL
    * https://api.twitter.com/2/tweets/:id
* Limitations
    * 900 requests per period (0: RL_TWEET_LOOKUP)
* Input
    * Tweet ID (SINGLE INPUT)
* Output
    * Tweet information about provided ID

<br />
<br />

### **TWEETS BY TWEET IDs (PLURAL)**

### *GET /2/tweets*
* Returns a variety of information about the Tweet specified by the requested ID or list of IDs.
* https://developer.twitter.com/en/docs/twitter-api/tweets/lookup/api-reference/get-tweets
* Endpoint URL
    * https://api.twitter.com/2/tweets
* Limitations
    * 900 requests per period (0: RL_TWEET_LOOKUP)
    * 100 tweets per request (output size is defined by number of input Tweet IDs)
* Input
    * Tweet ID(s), up to 100
* Output
    * Tweet information about provided ID(s)

<br />
<br />

### **TWEETS BY SEARCH QUERY**

### *GET /2/tweets/search/recent*
* Returns tweets from the last seven days matching a search query (can be restricted per-user, for example)
* https://developer.twitter.com/en/docs/twitter-api/tweets/search/api-reference/get-tweets-search-recent
* Endpoint URL
    * https://api.twitter.com/2/tweets/search/recent
* Limitations
    * 450 requests per period (3: RL_SEARCH_TWEETS_RECENT)
    * 100 results per page (max_results: 100 is maximum, 10 is default)
    * NO PAGINATION TOKEN! Can only advance to further pages through DIRECTLY CONSECUTIVE CALLS
* Input
    * Search Query
    * max_results (100 for maximum)
* Output
    * Tweet IDs of tweets (from the past 7 days) matching the provided search query

<br />
<br />

### **TWEET COUNTS BY SEARCH QUERY**

### *GET /2/tweets/counts/recent*
* Returns tweet COUNTS from the last seven days matching a search query (can be restricted per-user, for example)
* https://developer.twitter.com/en/docs/twitter-api/tweets/counts/api-reference/get-tweets-counts-recent
* Endpoint URL
    * https://api.twitter.com/2/tweets/counts/recent
* Limitations
    * 300 requests per period (5: RL_TWEET_COUNTS_RECENT)
* Input
    * Search Query
* Output
    * COUNT of tweets (from the past 7 days) matching the provided search query

<br />
<br />

### **LIST TWEETS LOOKUP**

### *GET /2/lists/:id/tweets*
* Returns recent tweets from the provided List ID
* https://developer.twitter.com/en/docs/twitter-api/lists/list-tweets/api-reference/get-lists-id-tweets
* Endpoint URL
    * https://api.twitter.com/2/lists/:id/tweets
* Limitations
    * 900 requests per period
    * 100 results per page (max_results: default 100, already maximum)
* Input
    * List ID (SINGLE INPUT)
    * pagination_token
* Output
    * Tweet IDs of up to 100 recent tweets from the list
