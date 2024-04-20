public | actor           | table    | postgres
 public | country         | table    | postgres
 public | director        | table    | postgres
 public | films           | table    | postgres
 public | genre           | table    | postgres
 public | producer        | table    | postgres
 public | year            | table    | postgres
 
# create producer scripts

create table producer (
	id integer,
	name text,
	PRIMARY KEY (id, name)
)

# create genre scripts

create table genre  (
	id integer,
	name text,
	PRIMARY KEY (id, name)
)

# create year scripts

create table year (
	id integer,
	year integer,
	PRIMARY KEY (id, year)
)

# create director scripts 

create table director (
	id integer,
	name text,
	PRIMARY KEY (id, name)
)

# create actor scripts 


create table actor (
	id integer,
	name text,
	PRIMARY KEY (id, name)
)

# create country scripts

create table country (
	id integer,
	name text,
	PRIMARY KEY (id, name)
)


# create films scripts 

create table films (
	id integer,
	name text,
	actor_id integer,
	country_id integer,
	director_id integer,
	genre_id integer,
	producer_id integer,
	year_id integer,
	PRIMARY KEY (id, name)
)


# querys

explain select name, 
	(select producer from producer where id = films.producer) as producer, 
	(select genre from genre where id = films.genre) as genre, 
	(select year from year where id = films.year) as year,
	(select director from director where id = films.director) as director,
	(select actor from actor where id = films.actor) as actor,
	(select country from country where id = films.country) as country
	from films;


	set enable_seqscan = off;