# Connie Coleman Jewlery Site

A website based on the [publify cms](https://github.com/publify/publify).

### Installing Locally (from the publify setup instructions)

To install Publify you need the following:

- CRuby (MRI) 2.1, 2.2 or 2.3
- Ruby on Rails 4.2.x
- A database engine, MySQL, PgSQL or SQLite3
- A compatible JavaScript installation for asset compilation. See [the execjs
  readme](https://github.com/sstephenson/execjs#readme) for details.
- ImageMagick (used by mini_magick).

1.  Clone the repo
2.  `cp database.yml.example database.yml`
3.  Edit database.yml to add your database name, login and password.
4.  Run:

```bash
$ bundle
$ rake db:setup db:migrate db:seed assets:precompile
$ rails server
```

You can now launch you browser and access 127.0.0.1:3000.

### Install Publify on Heroku

In order to install Publify on Heroku, you’ll need to do some minor tweaks.

First of all, you need to setup Amazon S3 storage to be able to upload files on
your blog. Set Heroku config vars.

```yaml
heroku config:set provider=AWS
aws_access_key_id=YOUR_AWS_ACCESS_KEY_ID
aws_secret_access_key=YOUR_AWS_SECRET_ACCESS_KEY
aws_bucket=YOUR_AWS_BUCKET_NAME
```

To generate the Gemfile.lock, run:
```bash
HEROKU=true bundle install
```

Remove Gemfile.lock from .gitignore and commit it.

Add the HEROKU config variable to your Heroku instance:

```bash
heroku config:set HEROKU=true
```

Push the repository to Heroku.

When deploying for the first time, Heroku will automatically add a Database
plugin to your instance and links it to the application. After the first
deployment, don't forget to run the database migration and seed.

```bash
heroku run rake db:migrate db:seed
```

If application error has occurred after migration, you need to restart Heroku server.

```bash
heroku restart
```
