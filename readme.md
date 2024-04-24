# create actor/director/producer/year(integer)/genre/country scripts 


create table actor (
	id integer,
	name text,
	PRIMARY KEY (id)
);
create index actor_frst_fk on actor (id) include (name);

# create films scripts 

create table films (
	id integer,
	name text,
	actor_id integer references actor (id),
	country_id integer references country (id),
	director_id integer references director (id),
	genre_id integer references genre (id),
	producer_id integer references producer (id),
	year_id integer references year (id),
	primary key(id, name, actor_id, country_id, director_id, genre_id, producer_id, year_id)
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


	-- set enable_seqscan = off;

	

	explain analyze select films.name, actor.name, director.name, year.num, producer.name, country.name, genre.name from films 
	left join actor on actor.id =  films.actor_id
	left join director on director.id =  films.director_id
	left join year on year.id =  films.year_id
	left join producer on producer.id =  films.producer_id
	left join country on country.id =  films.country_id
	left join genre on genre.id =  films.genre_id
	;


# Запросить фильм по жанрам

select films.name as films, actor.name as actor, director.name as director, year.num as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.id =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where films.genre_id in (select id from genre where name ilike '%4_gen%' or name ilike '%5_gen%');

# Запросить фильм по странам

select films.name as films, actor.name as actor, director.name as director, year.num as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.id =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where films.country_id in (select id from country where name ilike '%4_country%' or name ilike '%76_country%');

# Запросить фильм по режиссеру

select films.name as films, actor.name as actor, director.name as director, year.num as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.id =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where films.director_id in (select id from director where name ilike '%4_director%' or name ilike '%76_director%');


# Запросить фильм по актерам

select films.name as films, actor.name as actor, director.name as director, year.num as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.id =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where actor.name in ('4_actor', '5_actor');

# Запрос фильмов по диапазону лет (или одному году)

select films.name as films, actor.name as actor, director.name as director, year.num as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.id =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where year.num in (3,6);