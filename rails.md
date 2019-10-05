## Model

Generating models:
```
$ rails g model Author name:string genre:string bio:text —no-test-framework
```

Adding migration columns:
```
$ rails g migration add_column_to_table name_column:datatype
```

Adding multiple columns:
```
$ rails g migration add_more_statistics_to_authors copies_sold:integer last_novel_written:string
```

Removing columns:
```
$ rails g migration remove_last_novel_written_from_authors last_novel_written:string 
```

Adding references:
```
$ rails generate migration AddAddressRefToContacts address:references
```

We can use scaffolding too:
```
$ rails generate scaffold Post title:string body:text
$ rails generate scaffold Comment post_id:integer body:text
```

Undo scaffold:
```
$ rails d scaffold post
```

Run migration:

```
$ rake db:migrate
$ rake db:rollback
```

## Datatypes

# Datatypes

https://github.com/rails/rails/blob/4-2-stable/activerecord/lib/active_record/connection_adapters/postgresql_adapter.rb#L76
https://github.com/rails/rails/blob/master/activerecord/lib/active_record/connection_adapters/postgresql_adapter.rb#L69


- binary: for storing data such as images, audio or movies
- boolean: for storing true or false values
- date: for storing the date only
- datetime: for storing the date and time into a column (handles timezone)
- decimal: for decimals
- float: also for decimals
- integer: for whole numbers
- bigint
- primary_key
- references
- string: for small data types such as title
- text: for long pieces of textual data, paragraphs
- Time
- timestamp: for storing date and time into a column (timezone dependent)
- json
- Jsonb
