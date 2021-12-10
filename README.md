# How to Deploy Your Phase 3 Sinatra App

This assumes you've developed your app fully and you expect to deploy your backend on heroku. Let's get started!

In your gemfile, replace the `sqlite3` gem with the `pg` gem (`pg` stands for `postgres`)

```
gem 'pg'
```

Next, change the `config/database.yml` file so that it uses postgres (at least for the production build).

```
production:
  adapter: postgresql
  database: my_database_production
  pool: 5
  timeout: 5000
```

If you'd like, you can integrate the `test` and `development` databases as well.

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
