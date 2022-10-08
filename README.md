# pax-anonimi-db
`pax-anonimi-db` is a layer on top of SQLite that allows to store data as fully encrypted incremental database operations in independent files.

It allows you to use SQLite in projects that require a database that can be readily synced, end-to-end encrypted, between different clients on file systems that do not support file modifications (such as Amazon S3).

It was developed for the [TBD] app to provide a safe, end-to-end encrypted way for users to sync their data to the cloud. 

## How it works
When you create a `pax-anonimi` database, an SQLite database is created. Every create/alter/insert/update operation generates a file with information about the operation. These files are called `animi`s and will never change again.

When you want to replicate a `pax-anonimi` database, simply load every `animi` in chronological order and your 2 databases are synced! Any changes to the database will create new `animi`s that need to by synced back to every `pax-anonimi` database.

A `pax-anonimi` database is protected with a secret key. You must specify this key when creating a new database and loading `animi`s. 

Once all `animi`s have been loaded, you should keep a copy of the generated SQLite database for faster loading. However, this database should remain on the user's machine _because it is not encrypted_. 
