# Full Details 
TG Mirror Leech Bot

- `Branch`: master

https://github.com/priiiiyo/tg-mirror-leech-bot

# Heroku Deploy

**Important Notes**
1. This Branch only for deploying, generate all your private files from master branch.
2. Use this branch to avoid suspension `OR` deploy master branch twice with same app name (check helper.sh for help). To stay up to date don't fill `UPSTREAM_REPO`, on each `dyno restart` you will get lastest commits from official repository or fill `UPSTREAM_REPO` by your public/private fork link and fetch manually then you can update your bot by `restart cmd` and `dyno restart`.
3. Don't delete .gitignore file.
4. Read all variables definitions from master branch readme.
5. Keep the programmer inside you away and follow the steps.

------

## With CLI

- Clone this repo:
```
git clone https://github.com/priiiiyo/mirror-leech-bot mirrorbot/ && cd mirrorbot
```
- Switch to heroku branch
  - **NOTE**: Don't commit changes in master branch. If you have committed your changes in master branch and after that you switched to heroku branch, the new added files will `NOT` appear in heroku branch.
```
git checkout heroku
```
- After adding your private data
```
git add . -f
```
- Commit your changes
```
git commit -m token
```
- Login to heroku
```
heroku login
```
- Create heroku app
```
heroku create --region us YOURAPPNAME
```
- Add remote
```
heroku git:remote -a YOURAPPNAME
```
- Create container
```
heroku stack:set container
```
- Push to heroku
```
git push heroku heroku:master -f
```

------

### Extras

- To delete the app
```
heroku apps:destroy YOURAPPNAME
```
- To restart dyno
```
heroku ps:scale web=0
heroku ps:scale web=1
```
- To set heroku variable
```
heroku config:set VARNAME=VARTEXT
```
- To get live logs
```
heroku logs -t
```

------

## With Github Workflow

1. Go to Repository Settings -> Secrets

![Secrets](https://telegra.ph/file/9d6ed26f8981c2d2f226c.jpg)

2. Add the below Required Variables one by one by clicking New Repository Secret every time.

   - HEROKU_EMAIL: Heroku Account Email Id in which the above app will be deployed
   - HEROKU_API_KEY: Your Heroku API key, get it from https://dashboard.heroku.com/account
   - HEROKU_APP_NAME: Your Heroku app name, Name Must be unique
   - CONFIG_FILE_URL: Copy [This](https://raw.githubusercontent.com/appeza/mirror-leech-bot/master/config_sample.env) in any text editor.Remove the _____REMOVE_THIS_LINE_____=True line and fill the variables. For details about config you can see Here. Go to https://gist.github.com and paste your config data. Rename the file to config.env then create secret gist. Click on Raw, copy the link. This will be your CONFIG_FILE_URL. Refer to below images for clarity.

![Steps from 1 to 3](https://telegra.ph/file/2a27cf34dc0bdba885de9.jpg)

![Step 4](https://telegra.ph/file/fb3b92a1d2c3c1b612ad0.jpg)

![Step 5](https://telegra.ph/file/f0b208e4ea980b575dbe2.jpg)

3. Remove commit id from raw link to be able to change variables without updating the CONFIG_FILE_URL in secrets. Should be in this form: https://gist.githubusercontent.com/username/gist-id/raw/config.env
   - Before: https://gist.githubusercontent.com/iamSMMH/9cce4a4b4e7f4ea47e948b2d058e52ac/raw/19ba5ab5eb43016422193319f28bc3c7dfb60f25/config.env
   - After: https://gist.githubusercontent.com/iamSMMH/9cce4a4b4e7f4ea47e948b2d058e52ac/raw/config.env

   - You only need to restart your bot after editing config.env Gist secret.

4. After adding all the above Required Variables go to Github Actions tab in your repository.
   - Select Manually Deploy to Heroku workflow as shown below:

![Select Manual Deploy](https://telegra.ph/file/cff1c24de42c271b23239.jpg)

5. Then click on Run workflow

![Run Workflow](https://telegra.ph/file/f44c7465d58f9f046328b.png)

**NOTE**: Don't edit variables from Heroku, if you want to edit simply do it in config.env from your gist, after it just restart your app.

