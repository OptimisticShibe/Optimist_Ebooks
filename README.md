# Bee Squad Bot

### *Personal Node.js adventure to amuse friends on Twitter*

---

## Overview

**What it does:** This bot produces and tweets an algorithmically-generated (usually) readable sentence made up of phrases taken from a large collection of source tweets elsewhere on twitter. It tweets every 30 minutes, 24/7, and will not post pictures, reply, @-mention others, or use hashtags.

**How does it work:**

1. Every 30 minutes, the bot runs off of a cronjob and collects up to 1,000 tweets from each of the source twitter accounts, one by one.

2. The entire tweet collection is then run through a Markov-chain algorithmic scheme to produce 10 new tweetable phrases.

3. These 10 tweets are filtered to remove hashtags, @-mentions, and other twitter-style addendums.

4. 1 of these 10 tweets is selected, and further filtered through a custom NSFW word filter that locates and replaces specific words and phrases with less crass alternatives.

5. The now-sanitized tweet is then potentially altered with any number of 'fun' adjustments to further randomize the final product. (e.g. All caps, random tweet shortening)

6. The final tweet is then tweeted by @BeeSquadBot on twitter, via *Twit* package and the Twitter API.

#### Newest (significant) Updates

##### Jun 8, 2018

* Created README
* Fixed NSFW filter
* Removed NSFW filter word source from repo
* Moved REGEX cleanups to external file
* Deleted defunct Markov file

---

### Big TODOs

* Improve error handling
* Export more of bot.js to external modules
* **Documentation**

---

## Repo Contents

##### bot.js

Main body of code. Performs tweet collection, regex & nsfw filtering, markov randomization, and actually sends tweet.

* Single active function call = `getTweets(T).then(tweetIt);` - Everything else cascades down from that.
* Function **filterTweet** uses regex (`tweetCleanup.js`) to clean up punctuation and extraneous links etc. from the tweets themselves
* Function **getTweets** uses *Twit* package to interface w/ Twitter's API, and collect tweets from (in this case) multiple accounts
* Function **tweetIt** rolls helper function **fillData** in to utilize the *Markov* package and actually build the eBooks tweets (using a promise chain), before ultimately tweeting it out through the bot's twitter
* Function **dropWordMath** is a (messy) silly function that randomly adds emoji to the tweet, cuts words or length off of the tweet, or capitalizes the whole thing

##### config.js

Config file with tokens & keys. Kept off the repo for obvious reasons

##### nsfwFilterEdits.js

Filter module specifically for removing NSFW words, and replacing them with SFW alternatives. NSFW list is an external module kept off of the repo.

##### tweetCleanup.js

External module containing regular expressions for twitter-junk filtering

##### user_accounts.js

Simple list of contributing twitter accounts + associated emoji for debug message purposes. Eventually hope to expand bot capabilities to randomly tweet 100% from a single source, and that will weigh into it.

---

Feel free to contact with questions. Cheers!

[![BeeSquadPic](https://cdn.discordapp.com/attachments/279406927140749313/916184920236384316/OYUP2gCc_400x400.png)](https://twitter.com/BeeSquadBot)
*\*art by [@SharpiBees](https://twitter.com/sharpibees)*
