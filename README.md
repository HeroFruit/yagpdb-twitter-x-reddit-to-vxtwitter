THIS IS A FORK FROM WOOVIE TO USE VXTWITTER/VXREDDIT
FOLLOWING IS NOT UP-TO-DATE 

# yagpdb-twitter-to-fxtwitter
Reposts user's posts with twitter(dot)com URLs to fxtwitter(dot)com for better embeds, mobile embeds, and overall better media playback performance.

## How does it work?
A user will make a post like:
```
Hey guys! Check out this great tweet: https://twitter.com/akamikeb/status/1636974830426771457?cxt=HHwWgsC-ne372bctAAAA
```

With this custom command, YAGPDB will then repost the user's post, like so:
```
@UserXYZ said: Hey guys! Check out this great tweet: https://fxtwitter.com/akamikeb/status/1636974830426771457?cxt=HHwWgsC-ne372bctAAAA
```
The only inconvenience for this is that the user cannot simply delete the post themselves since a bot made it. The solution then is to also track these reposts using `dbSet`, storing the bot's sent message ID as the key and the user's ID as the value. If the user wants to delete the post, they must then react with `❌` and the post will be deleted using a lookup of the message ID using `dbGet`, and comparing that with the ID of who reacted.

## Why?
Discord unfortunately embeds in a way that then causes the video to buffer usually about 3 seconds in and take anywhere from 10 seconds to 2 minutes to finish buffering. The buffering seems to be caused by attempts to select a higher/lower quality. The embeds also do not work on mobile Discord versions.

## How to use

Modify the emoji variable as you please, then install the custom commands in [YAGPDB in the management UI](https://yagpdb.xyz/manage). Each custom command file has a small comment header explaining how to properly configure them.

For instance, `repost.go.tmpl` has:
```
{{/* Trigger Type: Regex
Trigger: .*[^fvx]twitter.com.* */}}
```
This should match what you see on YAGPDB's Custom Command UI:
![image](https://github.com/Woovie/yagpdb-twitter-to-fxtwitter/assets/7304619/8ed27f8d-9de8-4386-ad13-9cb01fc3b135)
