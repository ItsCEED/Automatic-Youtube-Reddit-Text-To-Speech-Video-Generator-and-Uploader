# NO LONGER SUPPORTED. PLEASE DO NOT EMAIL THE GMAIL ACCOUNT LISTED IN THE VIDEO. YOU WILL GET NO RESPONSE.
# Due to a lack of time and general loss of interest/motivation I have decided to terminate development of this project. This means that # I will no longer be providing the setup service and will not be replying to any emails. Thanks to all who took interest in the project.

# Automatic-Youtube-Reddit-Text-To-Speech-Video-Generator-and-Uploader

Following the recent YouTube trend in “Reddit to Text-To-Speech” YouTube Videos I embarked on a project to create a program that can automate the process of receiving, generating and uploading these videos to YouTube with as little intervention as possible. It took 4 months to finish the project and is comprised of 3 separate programs that work simultaneously in order to complete this task.

The idea was to minimize as much manual intervention as possible and automate all the trivial tasks. However the process cannot be 100% automated. For example comments with links in them cannot be kept as quality of the video will be comprised due to the TTS. Additionally while a comment might have a large number of votes it could potentially be offensive and not safe for a YouTube video and thus must be removed. The thumbnail, while partially generated, must be edited in order to create any kind of appeal to viewers to click on your video. The same goes for the title of the video which must be clickbait-y in order to receive any attention. I have attempted to streamline the manual process with the client program and it takes me approximately 30 minutes to create 6 videos (the max that can be uploaded within 24 hours with the YouTube Data API).

<h1>My Automatic Text To Speech Channel (Royal Reddit)</h1>
https://www.youtube.com/channel/UC0COfXvVMHVgZ-YH65Q8rVA?view_as=subscriber

**Some of my Generated Videos:**

https://www.youtube.com/watch?v=xxDKMHYXCsQ

https://www.youtube.com/watch?v=AW0yJIXXNxI&t=35s


**The process of completing a video involves:**

1.	Loading up the client program
2.	Selecting a raw script to edit
3.	Pressing keep/skip for each comment within the video
4.	When estimated video time is acceptable click publish video.
5.	Amend the title to be as clickbait as possible
6.	Add in some additional tags to suit to the video topic
7.	Edit the generated thumbnail in the thumbnail folder location and then select it
8.	Edit the description if you wish
9.	Press “Send To Video Generator” and you will be notified when the script has been finished uploading to the server
10.	Done

*Example Reddit Text-To-Speech Channels:*

https://www.youtube.com/watch?v=izSxHx64pGQ
https://www.youtube.com/watch?v=vzdTuAp2zTw

<h2>Assets Download For Video Generator Client http://www.mediafire.com/file/hpu1j1k1avwp9dj/YouTube_Bot_Assets.zip/file (500MB)</h2>

Place these in a folder called "Assets" within the YouTube Bot Video Generator directory.


<h2>DISCLAIMER</h2>
You will need to change several things for this code to work with your setup. The Video Generator Client and Server Program will be able to run on Linux. I rushed several parts of the project while balancing a full-time job so I could complete it before I started University in September. Additionally, I did not intend for it to be released to the public. That being said, I wouldn’t say its spaghetti code as I have several years of coding experience under my belt, however I am self-taught and thus I am sure that there are several aspects of the code that are not as efficient as possible and could have been designed much better.

API logins and keys are hardcoded into the code and must be located and changed manually to get it to work for your setup. I have created a list of locations where they can be found. (see below)

Furthermore I changed my mind on many design aspects partially through the project and therefore some files are named strangely and there is unused code here and there. I will not be updating the code anymore, however please feel free to.

<h2>Why Am I releasing this?</h2>
The motivation behind this project was to “bank” on YouTube advertisement money by spamming YouTube with a large quantity of these videos and then sitting back and letting the ad money build up.
In reality, I had not done my research well enough and it turns out that recent policy changes meant that channels comprising of mainly Text-To-Speech videos were flagged as “automated content” which would mean that I would likely fail to be approved for monetization: in the case that I do pass the monetization test, my individual videos could still be demonetized.
However saying this, this policy change is unclear and I am unsure whether it it is definite that you will not be able to get monetization.
With active server costs £32 a month and no guarantee that these videos will ever make money I decided it would be best to let the project go so I can work on new things in the future. Hence the reason why I am uploading it to GitHub.

<h2>Dependencies</h2>

**Client:**
PyQt5, cv2, PIL, numpy

**Video Generator Client:**
pydub, oauth2client, soundfile, pymediainfo, cv2, moviepy, PIL, numpy, matplotlib

YouTube-Upload https://github.com/tokland/youtube-upload

Balabolka http://www.cross-plus-a.com/balabolka.htm

Instructions on how to get the Daniel MLG Voice https://www.youtube.com/watch?v=yj3dhTnyotY

**YouTube Bot Server:**
Mysql-connector, praw

**Other**
MySql Server

Reddit account with developer key https://www.reddit.com/dev/api/ 

Google API account

<h2>How can a Video Possibly Generated by a Program and still be watchable?</h2>

This recent trend in Reddit Text-To-Speech Videos consists (usually) of a very simple formula:

1.  A sentence of text is revealed.
2.  Text To Speech reads out said sentence.
3.  Once the Text To Speech is complete, the next sentence of text is revealed.
4.  Repeat till comment and its replies are done.
5.  Once a comment and all if its subsequent replies are finished play some kind of transition interval.
6.  Move onto next comment
7.  Repeat steps 1-6 till you have a 10 minute video.

A song is chosen at random. I have downloaded ~40 songs Kevin MacLeod Royality Free Songs to be randomly choosen.

https://www.youtube.com/watch?v=ccpyyrdS-Qo&list=PLbzGR7H3FyUS3LvitxTFAIgv601UKUHjX

All assets used in the generation of the video can be downloaded here:

http://www.mediafire.com/file/hpu1j1k1avwp9dj/YouTube_Bot_Assets.zip/file

They must be placed in a folder called "Assets" in the Video Generator program.

<h2>How it works</h2>

The project is comprised of three separate programs:


1.  YouTube Bot Server -> initserver.py
2.	YouTube Bot Video Generator Client -> youtubequeue.py
3.	YouTube Bot Client (Manual Review) -> client.py

<h2>YouTube Bot Server</h2>

This program houses the (1) socket server for connecting to the client(s) program and also the (2) socket server for connecting to the video generator client(s). Additionally, this program will also grab new scripts from Reddit every one hour, and will also update the existing ones that have not yet been edited.

(1)	This socket server will send raw scripts from the database to the manual review program (see below). It will then receive these reviewed scripts and update the database with the finalised scripts which will include a thumbnail, description and title. The server can handle multiple clients so multiple people can edit these scripts.

(2)	The video generator server is currently only designed to handle one video generator client. Original plans were for this server to handle multiple video generator clients spread out between multiple computers. However, I found that one computer was sufficient enough for all my video generation needs, so mid-way through programming this I decided to hard code it to only handle one client. The purpose of this server is to send finalised scripts from the database to the video generator client.

<h2>YouTube Bot Video Generator Client</h2>

This program will receive finalised video scripts from the YouTube Bot Video Generator Server which include thumbnails, descriptions, tags and a title. These scripts will be generated into a mp4 file and then uploaded to YouTube at a scheduled release time (currently randomly at 5pm, 6 pm, 7pm GMT - the recommended times to upload to YouTube). Once the script is received it will be generated then the program will wait till it has enough API credits to upload by checking when the last 6 videos were uploaded. 

**API quota usage resets at 8am GMT**. I have calculated that uploading each video will cost **1658 credits**. You can use a maximum of 10 000 credits a day. This means in theory you will be able to **upload 6 videos a day**. However, in practise I have been able to upload 5 videos, sometimes the sixth one will upload however there will not be enough quotas available to upload the thumbnail, which in that case will require manual intervention to upload the thumbnail manually. The videos are uploaded with YouTube-Upload which I have only managed to get to work with python 2.7. It is called with subprocess.check_call with python version specified and arguments as required (link below).

Once a video is successfully uploaded its status is set to complete along with an upload time so that the program can check how many videos were uploaded within the day to avoid exceeding quota usage. 

YouTube Data API Information https://developers.google.com/youtube/v3/getting-started 
YouTube-Upload (python 2.7) https://github.com/tokland/youtube-upload

**Text-To-Speech**
By far one of the most challenging aspects of the project was getting the Text to Speech to work properly. I wanted to use the Daniel MLG Soft Scan Text to Speech voice – the one found in most text to speech Reddit videos. I believed this was an important part of the project because this voice is very recognisable and is (in my opinion) one of the best sounding text to speeches available.
I use the command line version of Balabolka to generate the .wav files and these were then synced with different frames in the video generation program.

Balabolka http://www.cross-plus-a.com/balabolka.htm
Instructions on how to get the Daniel MLG Voice https://www.youtube.com/watch?v=yj3dhTnyotY

<h2>YouTube Bot Client</h2>

The client program is a Tinder-like swipe left and right process to filter out comments that are not to be included in the video. It also allows for the user to write the title and upload a thumbnail for the video as well as edit description and tags, although the title, description and tags are partially generated as follows:
Title: Be default is the post title
Description: By default is a generated template with the post title within it and a couple hashtags
Tags: Some base tags I got from popular text-to-speech channels such as r/askreddit,reddit,reddit funny etc.
All of these can be edited. A template for the thumbnail is partially generated as well. There are checks to make sure that the amount of characters are not exceeded for all of these fields e.g. title must be under 100 characters

The final content of the video includes the edited script, the thumbnail, tags, description and the video settings (it is possible to change certain features of the video generator template during the editing process such as background colour, text size, line widths etc. I usually kept the defaults so didn’t really have much use for it) which is then sent off to the server which in turn uploads it to the database as a BLOB.

**MySQL**

Storage of the scripts and they’re relevant information is done with a MySQL database. This is the first time I used a MySQL database for a project, I’m not brilliant at SQL I learned what was necessary to get things to work. I used three tables “users”, “videogenerators” and “scripts”<br>

**“users” table**<br>
Originally I had planned to create a extensive login system where users had editing statistics, see who’s online etc. Scrapped this and now its only use is for keeping track of which users are editing which videos to prevent the same video being edited and uploaded twice. Passwords are encrypted with MD5 on the client side

**“scripts” table**<br>
The most important table, holds all the script information. The status field is very important for keeping track of where a script should be.
<br>*-raw:* the script is available to edit
<br>*-editing:* the script is being edited and cannot be edited by any other users while in this state
<br>*-complete:* the script has been finished editing and will be sent to the video generator client 
<br>*-successupload:* the script has successfully been uploaded to YouTube

**“videogenerators” table**<br>
Like the users, I designed the client to have a username and password to login. Password is encrypted with MD5 on the client side

These tables will be automatically created within a database called “youtubebot” if they do not already exist.

<h2>Receiving Reddit Scripts</h2>
I used praw to get the reddit scripts. By default I have set it to get 45 scripts from the hot tab on r/AskReddit. The minimum number of comments per script must be 1000. It will take 30 of the highest rated comments from each post, and five of subsequent highest rated replies to each comment. The code for this is located in the YouTube Bot Server under reddit.py
Be default on start up of the YouTube Bot Server, it will request scripts, then it will request every one hour after this. If the script is already in the database it will update the database script entry with the updated comments/upvote values.


Receive credentials for your google API account will be downloaded and saved automatically following a one time login (your browser window will be opened requesting a google account login): videouploader.py -> get_credentials()


