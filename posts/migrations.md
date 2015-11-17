# Migrations

 * What migrations are
 * How they affect schema.rb
 * Onboarding new devs should use rake db:setup
 * Reseting DB, rake db:reset
 * Seeds - app critical data you need
 * Break out into multiple files
 * Pushing changes through a pipeline
 * Keeping seeds up to date
 * Make seeds indomepedant
 * Graveyarding migrations

Are you able to delete all of your migrations in your Rails app, drop your database and get up and running again in less than a minute or two? If the answer is no, then that means you're probably not treating the data your app depends on seriously enough.

Migrations are a means to alter your database schema, but also potentially alter the data contained within it too. As you're building your app, you write migrations as you go along. When you run `rake db:migrate`, your `db/schema.rb` file is updated to reflect your current schema. When you run a migration, the changes are applied in this file, and then the version is updated at the top to reflect the timestamp of the latest migration.

When you or another developer wants to work on the project, they should be able to just run `rake db:setup` in order for your database to be created, and for the current version of your schema to be setup too. There's no need to run through `rake db:migrate` for a fresh project clone, as `schema.rb` is the single source of truth.

As you continue to develop the project in a team, you'll use `rake db:migrate` to get the latest changes.

Along with a database schema, your app probably also depends on a set of data being present in the database for it to function. This is app critical. It might be a list of categories, or an admin user for example. You might either use a migration to populate this data, or do this manually via an admin interface or the Rails console. But the thing to keep in mind is that your `schema.rb` file is only used for your db structure. Any data you add to the database, isn't persisted anywhere. So if you have to reset your database, or someone new works on the project, if they run a `rake db:setup` they'll get a DB with the correct structure and zero data.

This is where `seeds.rb` comes in. This file is to data what `schema.rb` is for structure. The difference though is that you have to manage this file yourself. When you create a migration that alters the data somehow, Rails won't be updating the `seeds.rb` file for you.

When you run `rake db:setup` or `rake db:reset` Rails will create/empty your database, load your current schema, and then run the `seeds.rb` file to populate  it. So by keeping your `seeds.rb` file in sync with the data your app requires, with a single command, you can get yourself or others up to speed much quicker.

You should try and write your seed code so that it's idempotent. That is, if you run it multiple times, you won't get duplicated data added. If you're using ActiveRecord, that's where `find_or_create_by!` comes in very handy.

This isn't to say that you should stop writing migrations to get your data into your database. You probably have a Continuous Delivery pipeline (right?) where you need to get seed data up to your production environment. Put that in a migration. But just be sure to make sure that code 
