# Twitter Trending Topics

For this assessment you will build a Spark based solution to discover trending topics in Twitter data. Obviously, Twitter provides this feature already, yet having your own implementation may come in handy. The [Twitter trending topics](https://en.wikipedia.org/wiki/Twitter#Trending_topics) feature is bound to geographical areas, such as countries or cities, whereas for different purposes you may want to determine trending topics amongst arbitrary groups of Twitter users. For example all the followers of your corporate account or networks of people that are somehow of special interest to you.

## Assignment
Trending is something that usually is updated in real-time or (more realistically) near real-time. While this provides obvious benefits, we will focus for this assignment on determining trending topics in batch based on a available dataset, which was captured over a period of time. The assignment will be to create one or more Spark jobs that take a set of Twitter data as input and produce a top 5 of trending topics per day.

### Bonus
Build it such that it can do top N trending topics per arbitrary amount of time (i.e. the same code could do top 3 per hour as well as top 10 per day).

### Trending
We will loosely define trending topic for a period in time as: words or phrases of which the [slope](https://en.wikipedia.org/wiki/Slope) of the frequency of occurence is largest during said period in time. Bonus: You can experiment with alternative (more realistic) algorithms, sliding windows and / or decay functions.

What constitutes a word or phrase and whether the distinction between the two should be made is open for interpretation. So, you can get all fancy and do stop word removal, determine that certain combinations of words should be counted as one, do spell checking to classify duplicates, etc., or just split strings on whitespace. It is adviseable to start out with the simplest possible thing.

### Implementation and end result
Please take into account software engineering practices. The end result should be a python package that can be deployed to a Hadoop cluster.

### Data
A status message looks like this (but without the line breaks and formatting):

```javascript
{
  "coordinates": null,
  "created_at": "Sat Sep 10 22:23:38 +0000 2011",
  "truncated": false,
  "favorited": false,
  "id_str": "112652479837110273",
  "entities": {
    "urls": [
      {
        "expanded_url": "http://instagr.am/p/MuW67/",
        "url": "http://t.co/6J2EgYM",
        "indices": [
          67,
          86
        ],
        "display_url": "instagr.am/p/MuW67/"
      }
    ],
    "hashtags": [
      {
        "text": "tcdisrupt",
        "indices": [
          32,
          42
        ]
      }
    ],
    "user_mentions": [
      {
        "name": "Twitter",
        "id_str": "783214",
        "id": 783214,
        "indices": [
          0,
          8
        ],
        "screen_name": "twitter"
      },
      {
        "name": "Picture.ly",
        "id_str": "334715534",
        "id": 334715534,
        "indices": [
          15,
          28
        ],
        "screen_name": "SeePicturely"
      },
      {
        "name": "Bosco So",
        "id_str": "14792670",
        "id": 14792670,
        "indices": [
          46,
          58
        ],
        "screen_name": "boscomonkey"
      },
      {
        "name": "Taylor Singletary",
        "id_str": "819797",
        "id": 819797,
        "indices": [
          59,
          66
        ],
        "screen_name": "episod"
      }
    ]
  },
  "in_reply_to_user_id_str": "783214",
  "text": "@twitter meets @seepicturely at #tcdisrupt cc.@boscomonkey @episod http://t.co/6J2EgYM",
  "contributors": null,
  "id": 112652479837110273,
  "retweet_count": 0,
  "in_reply_to_status_id_str": null,
  "geo": null,
  "retweeted": false,
  "possibly_sensitive": false,
  "in_reply_to_user_id": 783214,
  "place": null,
  "source": "<a href=\"http://instagr.am\" rel=\"nofollow\">Instagram</a>",
  "user": {
    "profile_sidebar_border_color": "eeeeee",
    "profile_background_tile": true,
    "profile_sidebar_fill_color": "efefef",
    "name": "Eoin McMillan ",
    "profile_image_url": "http://a1.twimg.com/profile_images/1380912173/Screen_shot_2011-06-03_at_7.35.36_PM_normal.png",
    "created_at": "Mon May 16 20:07:59 +0000 2011",
    "location": "Twitter",
    "profile_link_color": "009999",
    "follow_request_sent": null,
    "is_translator": false,
    "id_str": "299862462",
    "favourites_count": 0,
    "default_profile": false,
    "url": "http://www.eoin.me",
    "contributors_enabled": false,
    "id": 299862462,
    "utc_offset": null,
    "profile_image_url_https": "https://si0.twimg.com/profile_images/1380912173/Screen_shot_2011-06-03_at_7.35.36_PM_normal.png",
    "profile_use_background_image": true,
    "listed_count": 0,
    "followers_count": 9,
    "lang": "en",
    "profile_text_color": "333333",
    "protected": false,
    "profile_background_image_url_https": "https://si0.twimg.com/images/themes/theme14/bg.gif",
    "description": "Eoin's photography account. See @mceoin for tweets.",
    "geo_enabled": false,
    "verified": false,
    "profile_background_color": "131516",
    "time_zone": null,
    "notifications": null,
    "statuses_count": 255,
    "friends_count": 0,
    "default_profile_image": false,
    "profile_background_image_url": "http://a1.twimg.com/images/themes/theme14/bg.gif",
    "screen_name": "imeoin",
    "following": null,
    "show_all_inline_media": false
  },
  "in_reply_to_screen_name": "twitter",
  "in_reply_to_status_id": null
}
```