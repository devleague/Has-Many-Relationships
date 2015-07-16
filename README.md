# Has Many Relationships

When connecting to your pg database, connect from this project directory.

To run sql statements from an external file, use the \i [filepath] command.

### SQL 1-n Relationships and Joins Exercise in PostgreSQL


## Setup schema and relationships

1. Create a new postgres user named `has_many_user`
1. Create a new database named `has_many_blogs` owned by `has_many_user`
1. Before each create table statement, add a drop table if exists statement.
1. In `has_many_blogs.sql` Create the tables (including any PKs, Indexes, and Constraints that you may need) to fulfill the requirements of the **has_many_blogs schema** below.
1. Create the necessary FKs needed to relate the tables according to the **relationship table** below.
1. Run the provided `scripts/blog_data.sql`


## has_many_blogs schema

### users

| Column Name  | Datatype                | NULL  | Default           |
|--------------|-------------------------|-------|-------------------|
| id (PK)      | serial                  | false | auto incrementing |
| username     | character varying (90)  | false |                   |
| first_name   | character varying (90)  | true  | NULL              |
| last_name    | character varying (90)  | true  | NULL              |
| created_at   | timestamp (with tz)     | false | now()             |
| updated_at   | timestamp (with tz)     | false | now()             |

### posts

| Column Name  | Datatype                | NULL  | Default           |
|--------------|-------------------------|-------|-------------------|
| id (PK)      | serial                  | false | auto incrementing |
| title        | character varying (180) | true  | NULL              |
| url          | character varying (510) | true  | NULL              |
| content      | text                    | true  | NULL              |
| created_at   | timestamp (with tz)     | false | now()             |
| updated_at   | timestamp (with tz)     | false | now()             |

### comments

| Column Name  | Datatype                | NULL  | Default           |
|--------------|-------------------------|-------|-------------------|
| id (PK)      | serial                  | false | auto incrementing |
| body         | character varying (510) | true  | NULL              |
| created_at   | timestamp (with tz)     | false | now()             |
| updated_at   | timestamp (with tz)     | false | now()             |


## Relationship Table

| Table Name   | Relationship            | Table Name   |
|--------------|-------------------------|--------------|
| users        | Has Many                | posts        |
| users        | Has Many                | comments     |
| posts        | Has Many                | comments     |
| posts        | Belongs To              | users        |
| comments     | Belongs To              | users        |
| comments     | Belongs To              | posts        |

Reading relationship information in a table format can be difficult, whiteboarding the the relationship model in UML/ERD format is ~~highly recommended~~ required.

## Queries across multiple tables

Write the following SQL statements in `joins.sql`

1. Create a query to get all fields from the `users` table
1. Create a query to get all fields from the `posts` table where the `user_id` is 100
1. Create a query to get all posts fields, the user's first name, and the user's last name, from the `posts` table where the user's id is 200
1. Create a query to get all posts fields, and the user's username, from the `posts` table where the user's first name is 'Norene' and the user's last_name is 'Schmitt'
1. Create a query to get usernames from the `users` table where the user has created a post after January 1, 2015
1. Create a query to get the post title, post content, and user's username where the user who created the post joined before January 1, 2015
1. Create a query to get the all rows in the `comments` table, showing post title (aliased as 'Post Title'), and the all the comment's fields
1. Create a query to get the all rows in the `comments` table, showing post title (aliased as post_title), post url (ailased as post_url), and the comment body (aliased as comment_body) where the post was created before January 1, 2015
1. Create a query to get the all rows in the `comments` table, showing post title (aliased as post_title), post url (ailased as post_url), and the comment body (aliased as comment_body) where the post was created after January 1, 2015
1. Create a query to get the all rows in the `comments` table, showing post title (aliased as post_title), post url (ailased as post_url), and the comment body (aliased as comment_body) where the comment body contains the word 'USB'
1. Create a query to get the post title (aliased as post_title), first name of the author of the post, last name of the author of the post, and comment body (aliased to comment_body), where the comment body contains the word 'matrix' ( should have 855 results )
1. Create a query to get the first name of the author of the comment, last name of the author of the comment, and comment body (aliased to comment_body), where the comment body contains the word 'SSL' and the post content contains the word 'dolorum' ( should have 102 results )
1. Create a query to get the first name of the author of the post (aliased to post_author_first_name), last name of the author of the post (aliased to post_author_last_name), the post title (aliased to post_title), username of the author of the comment (aliased to comment_author_username), and comment body (aliased to comment_body), where the comment body contains the word 'SSL' or 'firewall' and the post content contains the word 'nemo' ( should have 197 results )

### Additional Queries

If you finish early, perform and record the following SQL statements in `joins.sql` using these higher level requirements.

1. Find the post id, post title, and user id of all posts where the post author commented on his/her own post. ( should have 2 results )
1. Count how many comments have been written on posts that have been created after July 14, 2015 ( should have one result, the value of the count should be 25)
1. Find all users who comment about 'programming' ( should have 337 results)
