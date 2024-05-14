# create actor/director/producer/genre/country scripts 


create table actor (
	id integer,
	name text,
	PRIMARY KEY (id)
);
create index actor_frst_fk on actor (id) include (name);

# create scprit for table year

create table year (
	year serial primary key
)

# create films scripts 

create table films (
	id integer primary key,
	name text not null,
	actor integer[] not null,
	country integer[] not null,
	director integer[] not null,
	genre integer[] not null,
	producer integer[] not null,
	year integer not null
)

create index fk_films_actor on films (actor);
create index fk_films_country on films (country);
create index fk_films_director on films (director);
create index fk_films_genre on films (genre);
create index fk_films_producer on films (producer);
create index fk_films_year on films (year);

---
v3

select films.name as film, films.year as year, 
	actor.name as actor, director.name as director,
	producer.name as producer, country.name as country,
	genre.name as genre 
	from films

	join (select films_actor.films_id, actor.name from films_actor 
join actor on films_actor.actor_id = actor.id) actor on actor.films_id = films.id 
	join (select films_director.films_id, director.name from films_director 
join director on films_director.director_id = director.id) director on director.films_id = films.id 
	join (select films_producer.films_id, producer.name from films_producer 
join producer on films_producer.producer_id = producer.id) producer on producer.films_id = films.id 
		join (select films_country.films_id, country.name from films_country 
join country on films_country.country_id = country.id) country on country.films_id = films.id 
		join (select films_genre.films_id, genre.name from films_genre 
join genre on films_genre.genre_id = genre.id) genre on genre.films_id = films.id 
	;


# querys


# Запросить фильм по жанрам

explain analyze select films.name as films, actor.name as actor, director.name as director, year.year as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.year =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where genre.name in('76_genre', '77_genre');

# Запросить фильм по странам

explain analyze select films.name as films, actor.name as actor, director.name as director, year.year as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.year =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where country.name = '76_country';

# Запросить фильм по режиссеру

explain analyze select films.name as films, actor.name as actor, director.name as director, year.year as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.year =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where director.name = '76_director';


# Запросить фильм по актерам

explain analyze select films.name as films, actor.name as actor, director.name as director, year.year as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.year =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where actor.name = '4_actor';

# Запрос фильмов по диапазону лет (или одному году)

explain analyze select films.name as films, actor.name as actor, director.name as director, year.year as year, producer.name as producer, country.name as country, genre.name as genre from films 
left join actor on actor.id =  films.actor_id
left join director on director.id =  films.director_id
left join year on year.year =  films.year_id
left join producer on producer.id =  films.producer_id
left join country on country.id =  films.country_id
left join genre on genre.id =  films.genre_id
where films.year_id in (select year from year where year in(1970, 2024));