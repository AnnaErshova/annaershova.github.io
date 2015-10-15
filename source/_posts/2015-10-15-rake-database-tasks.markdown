---
layout: post
title: "Rake Database Tasks"
date: 2015-10-15 10:47:23 -0400
comments: true
categories: rake
---

There are multiple db namespace rake tasks, which are very useful for a Rails developer. 

I don't often see them covered in Rails tutorials as a task list, and it took me a while to figure out which commands I needed to use while developing.

Most beginner developers stick to `rake db:migrate`, `rake db:seed` and `rake db:reset`, but there are quite a few more options.

*Migration* is a version of a database (I *still* don't understand what we are migrating and where, but oh well, such is conventional terminology).

Each new migration modifies a database schema (which starts out blank) by adding and removing data, changing data types etc. 

Your schema is normally stored in  `db/schema.rb`, although for some developers, it will be in `db/structure.sql`.

(To create and use `structure.sql`, use `config.active_record.schema_format = :sql` in your `config/application.rb`. Most beginners should be sticking to schema.rb, the default version.)

First, some schema-related tasks:

* `rake db:version` - to see your current schema version. Schemar versions are normally also listed as timestamps, so you will see something like `Current version: 20151014015045`.

* `rake db:forward` will push the schema one step up.

* `rake db:schema:load` -- loads she schema into your database. Good practice is using it when you first put your app in production; then run migrations from there on.

* `rake db:schema:dump` -- dumps she schema.

Now back to migrations:


The easiest way to generate a migration is to run `rails g migration AddUseridToPosts user_id:integer`.

Once a migration has been generated, it will be listed in your `db/migrate` folder, usually with a format `datestamp_migration_name.rb`. Running `rails g` generates a timestamp prefix because that is the order that Rails uses to execute pending migrations.

If you are creating a migration manually or copying over from another file, you need to use any alphanumeric prefix (even if it's one 1,2, and 3) that allows Rails to run pending migrations in correct order; or use a manual datestamp if that's what your other migrations use.

The migration in the example above adds a new colume of `user_id`, which is a type `integer`, to a table named `Posts` -- assumption here is that one user `has_many` posts and a post `belongs_to` user (if you don't know what that means, see [Active Record Association Basics](http://guides.rubyonrails.org/association_basics.html) ). 

You can generate a migration to add a new table altogether, to remove a table or a column, to change a data type of a column, etc.

Even if the migration is in your migrate folder, it does not mean it is in the database schema yet. To incorporate it into the schema, you have any pending migrations into it. And that's when `rake db:migrate` task comes in.

Before I get started, see this [rails source](https://github.com/rails/rails/blob/master/activerecord/lib/active_record/railties/databases.rake) to see the database.rake file that describes exactly what each task does. 

Rake tasks undergo changes between different versions of Rails, so it's good to keep an eye out for anything that might be coming soon.

* `rake db:migrate` -- runs the change or up method for all pending migrationsone by one in order indicated by name prefixes. If there are no such migrations, running the task won't produce any outcome. But when there are, it also executes `db:schema:dump` as it needs to dump the schema and build it anew considering the migration(s) that have been added.

* `rake db:migrate VERSION=version_number/timestamp` -- runs specific migration to which the datestamp refers.

* NB: `rake db:migrate VERSION=0>` -- roll back all migrations

* `rake db:migrate RAILS_ENV=test` -- runs migrations in an indicated envrionment.

You should be able to get timestamp as a prefix to a migration file name if you used a rails g command as explained above.

* `rake db:migrate:up` -- runs up command for a given migration version (default is current version)

* `rake db:migrate:down` -- runs down command aka rolls back command for a given migration version

NB: `Up` and `down` are actually old-school commands; `up` makes a change to the schema and `down` reverses the `up` change.

* `rake db:migrate:redo` -- "Rollbacks the database one migration and re migrate up (options: STEP=x, version_number/timestamp)."

* `rake db:migrate:redo STEP=x` = rolls back x many migrations and re-runs them

* `rake db:migrate:rollback` -- roll back last migration to get user back one step.

* `rake db:migrate:rollback STEP=x` -- roll back x many steps

Now this is interesting:

* `rake db:migrate:reset` = `rake db:drop`+ `rake db:create` + `rake db:migrate` = undo and re-do migrations again for current environment. It does not rollback migrations.

Note the difference from: 

* `rake db:reset` = `rake db:drop` + `rake db:setup` 

where 

`rake db:setup` = `rake db:schema:load` OR `rake db:structure:load` + 'rake db:seed'

* (`rake db:schema:load` loads schema.rb into your database)

* (`rake db:structure:load` loads db/structure.sql if you have specified that in your config)

Which means that `rake db:reset` drops database; recreates it from `db/schema.rb` or `db/structure.sql` in your current environment (and NOT from migrations); seeds database from `seeds.rb`. 

*Note that `rake db:migrate:reset` won't seed your database and `rake db:setup` will.* 

Another rake task is also useful to see where you are with regard to migrations:

* `rake db:migrate:status` -- display status of all migrations. It will alert you if there are no schema migrations in your project yet.


And a heavy hitter:

* `rake db:purge` -- "Empty the database from DATABASE_URL or config/database.yml for the current RAILS_ENV (use db:drop:all to drop all databases in the config). Without RAILS_ENV it defaults to purging the development and test databases." 

(The `rake db:purge` task was only added in January 2014 and is less known still.)


There is a great Rails Guide explaining a lot of these [here](http://edgeguides.rubyonrails.org/active_record_migrations.html).

Remember to restart your rails server when working with these.

Should these tasks not meet your needs, you can always create a custom rake task to do exactly what you need.