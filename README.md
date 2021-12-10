# How to Deploy Your Phase 3 Sinatra App

This assumes you've developed your app fully and you expect to deploy your backend on heroku. Let's get started!

First, if you'd like to utilize postgresql in your local environment (you should) then install it via the command line. This can be done depending on the system but it'll either be:

```
Mac
brew install postgresql
```

or 

```
Linux/WSL
sudo apt install postgresql
```

In your gemfile, replace the `sqlite3` gem with the `pg` gem (`pg` stands for `postgres`)

```
gem 'pg'
```

Run the bundle install to generate a new `Gemfile.lock`. Go into the lock file and look for a line that looks like this:
```
PLATFORMS
  x86_64-darwin-21
```

If it doesn't have `x86_64-linux` then add that so it looks like this:

```
PLATFORMS
  x86_64-darwin-21
  x86_64-linux
```

WSL/Linux users may not need to make any changes.

Next, change the `config/database.yml` file so that it uses postgres:

```
development:
  adapter: postgresql
  database: my_database_development
  pool: 5
  timeout: 5000
test:
  adapter: postgresql
  database: my_database_test
  pool: 5
  timeout: 5000
production:
  adapter: postgresql
  database: my_database_production
  pool: 5
  timeout: 5000
```

At this point you ought to set up your repo so that it can push to a production build on heroku. You'll find the steps here: [link](https://devcenter.heroku.com/articles/getting-started-with-ruby#deploy-the-app)

In addition to those steps, run `heroku addons:create heroku-postgresql`

Finally, while heroku is almost set up, we manually need to migrate the database with:

```
heroku run rake db:migrate
```

You can also pre-seed the database with:

```
heroku run rake db:seed
```

That's it!

Once you've deployed your backend, you can now gather that endpoint from heroku and integrate it into your frontend like so: [link](https://devcenter.heroku.com/articles/getting-started-with-nodejs)

Resources:

[https://devcenter.heroku.com/articles/sqlite3](https://devcenter.heroku.com/articles/sqlite3)

[https://devcenter.heroku.com/articles/getting-started-with-ruby#deploy-the-app](https://devcenter.heroku.com/articles/getting-started-with-ruby#deploy-the-app)

[https://devcenter.heroku.com/articles/rake](https://devcenter.heroku.com/articles/rake)
