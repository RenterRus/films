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
	id integer,
	name text,
	actor_id integer,
	country_id integer,
	director_id integer,
	genre_id integer,
	producer_id integer,
	year_id integer,
	primary key(id, name)
)

create index fk_films_year on films (year_id)

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