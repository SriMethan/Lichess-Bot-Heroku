# lichess-bot

Engine communication code taken from https://github.com/ShailChoksi/lichess-bot by [ShailChoksi](https://github.com/ShailChoksi)

### Chess Engine

- [Stockfish Multi Variant (dev)](https://github.com/ddugovic/Stockfish)

### Heroku Buildpack

- [`heroku/python`](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-python)

### Heroku Stack

- [`heroku-20`](https://devcenter.heroku.com/articles/heroku-20-stack) (allowing a maximum hash size of 512 mb)

### How to Use

- [Fork](https://github.com/SriMethan/lichess-bot-heroku/fork) this repository.
- Edit only your token in the `config.yml` file over [here](/config.yml#L1).
- Create a [new heroku app](https://dashboard.heroku.com/new-app).
- Go to the `Deploy` tab and click `Connect to GitHub`.
- Click on `search` and then select your fork of this repository.
- Then `Enable Automatic Deploys` and then select the `main` branch (which is already done by default usually) and Click `Deploy`.
- Once it has been deployed, go to `Resources` tab on heroku and enable `worker (bash startbot.sh)` dynos. (Do note that if you don't see any dynos in the `Resources` tab, then you must wait for about 5 minutes and then refresh your heroku page.)

You're now connected to lichess and awaiting challenges! Your bot is up and ready!

### Important Notes

- This code might result in many crashes, so if any error shows up in the logs, immediately restart all dynos by clucking on `more` in the top right corner of your heroku app and then click `restart all dynos`. Also do [create an issue](https://github.com/SriMethan/lichess-bot-heroku/issues/new) with your error logs if it has not already been discussed in another issue.
- Do note that on heroku you are allowed a maximum of 550 hours a month, so you can't run your bot 24/7 unless you have a verified account. To get a verified account you will need to provide your payment details, but no payment is required. Once this is done, your account becomes verified and you are provided an additional 450 hours a month which sums up to a total of 1000 hours a month which is more than what is needed to run your bot 24/7 on lichess.
- This bot uses `256 MB hash size` with `10 threads` (stack: `heroku-20`). This is quite strong. Heroku's free dyno's limitations are crossed even with 2-3 games in one go. So make sure you don't play many games in one go. If you want multiple games at a time, reduce the values of threads and hash in the [`config.yml` file](/config.yml#L14-L15) and use multithreading to handle multiple games. This is mainly caused due to rate limiting from heroku. This can be prevented by decreasing the hash and threads in the [`config.yml` file](/config.yml#L13-L14).
- When changing engines make sure you rename your engine name in the [`startbot.sh` file, line 2](/startbot.sh#L2) with `chmod a+x engines/engine-name`, where `engine-name` must be replaced with the name of your engine. If your engine name is the same after changing your engine, this doesn't need to be done. Also do note forgot to change the engine name in the [config.yml file](/config.yml#L6) too, where `name: "SF"` must be changed to `name: "engine-name"`, where `engine-name is the name of your engine. All engines must be placed in the [engines folder](/engines).
