# Bitwarden_rs on Heroku for Free!
Deploy Bitwarden_rs in Heroku for free via Github1

![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/davidjameshowell/bitwarden_rs_heroku/BitwardenRSOnHerokuAIO/deploy?label=Deploy%20Bitwarden_RS&style=for-the-badge)
![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/davidjameshowell/bitwarden_rs_heroku/BitwardenRSOnHerokuAIO/main?label=Update%20Bitwarden_RS&style=for-the-badge)

## Features
* Build and deploy cutomized Bitwarden_rs image from source to Heroku via Github actions
* Add global Duo Security enablement for replica deployment as needed
* Maintanable updates with Git Hash for future updates
* Easily extendable for future tweaks

## Usage

Usage is simply, fast, and user friendly!

### Deployment

1. Create a fork of this project
2. Create a new `deploy` branch with current forked contents of `main` branch.
3. Edit the `.github/workflows/main.yml` to enable/disable Duo and/or modify the checkout hash of bitwarden_rs upstream.
4. Go to your forked repo Settings > Secrets and add secrets for:
  * HEROKU_EMAIL (the email you used to sign up for Heroku)
  * HEROKU_API_KEY (yoru Heroku API key - can be found in **[Account Setings](https://dashboard.heroku.com/account)** -> APi Keys)
  * HEROKU_APP_NAME (the name of the Heroku application, this must be unqiue across Heroku and will fail if it is not)
5. Commit and push your deploy branch back to your forked repo.
6. Github Actions will run the job and begin deploying the app. This will take around 15 minutes.
7. Congrats, you now having a fully functional Bitwarden_rs instance in Heroku!
 
 ### Update
 
 Updating is simple and can be done one of two ways:
 * Running the workflow manually via Github Actions
 * Making a commit to the main branch, forcing a Github Actions workflow to initiate
 
Either one of these will force the Github Actions workflow to run and update the app. If you need to modify to enable/disable settings, you shoudl re run it as well.

## Why this was started
In **[this issues request](https://github.com/dani-garcia/bitwarden_rs/issues/954)**, someone had inquired if it was possible to install Bitwarden_rs in Heroku. Unfortunately the dev team had not done this before and someone had tried but was unsccessful (due to port binding issues).

As my Bitwarden instance is a critical part of my daily workflow and part of acceptance from users in my group whom I need to share passwords with, high availability services are also an important part. I run a replica of Bitwarden on a cheap cloud server where I also take backups as well to S3, but seeing Heroku have a generous free tier, I was inclined to try this out!

# Notes to consider

Your Bitwarden instance will go to sleep after 30 minutes of no activity. This should not be too bad of an issue due to the fact that you can maintain a local copy. However if you are adding, you may wish to have a cron job which polls your instance to keep it avaliable (read: Pingdom set to 15 minute intervals or any website status checker).

The JawsDB instance comes with 5MB of storage space. I found this sufficient enough for my own personal backups even with 700+ entries, two orgs, and 4 members. You may find if you are attaching content, that you might exceed this but I suggest attach files in base64 encoded content to preserve portability.