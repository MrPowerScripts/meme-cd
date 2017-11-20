# Continuous Meme Delivery

[Youtube VIDEO: Continuous Meme Delivery](https://youtu.be/oHaYyZgiDIU)

## Probably the most pointless thing I've ever put together

### How it works

Continuous Integration and Continuous Deployment are two software development paradigms
that streamline the process between committing your code changes and making those changes
accessible to your users. Ensuring that your software maintains a high standard of quality by automatically
running all of your tests (lol tests) against every change you make and quickly deploying those changes
when they've passed the quality checks. It is a process now used by every major software development company to ensure that mission critical software is delivered as quickly as possible without unexpected problems arising after deployment.

This repository uses it to upload a Meme to Reddit.

There are many CI/CD tools available to use. Travis, Jenkins, Drone.io, Codeship. For this example we will
use CircleCI.

You can view the builds run by this repository [here on the CircleCI website](https://circleci.com/gh/MrPowerScripts/meme-cd).

The Meme image is in the root of the repository as `meme.png`. All of the magic occurs inside of the config.yml. It contains the instructions that perform some basic testing on the image, uploading that image to Imgur, and then posting it as a link post to a subreddit.

Imgur, Reddit, and Github accounts are of course required. Also registering an application on Imgur and Reddit so that we can use their API.

Registering an Imgur app can be done here https://api.imgur.com/oauth2/addclient

Registering a Reddit app can be done here https://www.reddit.com/prefs/apps/

Once you've registered your apps you'll be given a client_id and client_secret. These details
are added into the CircleCI website as environment variables, so that we don't expose them in the repository. Reddit also requires that you include your reddit username and password for write access.

[This two minute video](https://www.youtube.com/watch?v=KhjwnTD4oec) shows how to setup the
meme-cd repository to your CircleCI account so that you can add the Environment Variables,

Adding environment variables for the project on CircleCI can be done here
(note to change the username to your GitHub username)
https://circleci.com/gh/mrpowerscripts/meme-cd/edit#env-vars

The required enviroment  variables to set in CircleCI are:
```
IMGUR_CLIENT_ID
IMGUR_CLIENT_SECRET
REDDIT_CLIENT_ID
REDDIT_CLIENT_SECRET
REDDIT_USERNAME
REDDIT_PASSWORD
```

Once all that is set up you can deploy a Meme to the subreddit of your choosing by editing the additional Environment Variables set near the top of the config.yml. You can edit the TITLE to choose
the name of your post.

```
environment:
  - TITLE: "My Meme"
  - SUBREDDIT: "mrpowerscripts"
```

The config.yml is set to only run a deployment when you push a tag. So you can manage different
Memes in different branches and push them without accidentally deploying. When you want to deploy a Meme simply create a tag `git tag my-meme` and push it up to your repository. This will run some basic checks on the image and then perform the deployment.
