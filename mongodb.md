# INTRODUCTION MONGO DB

## MONGO DB TOOLS
 1. [COMPASS]<https://www.mongodb.com/download-center/compass?jmp=hero>
 2. [SHELL]<https://www.mongodb.com/download-center/community>
 3. [MONGODB CLOUD] <https://cloud.mongodb.com>

## COMMANDS MONGO SHELL

 * <strong>CONNECT</strong>:
 	```mongo "mongodb://cluster0-shard-00-00-jxeqq.mongodb.net:27017,cluster0-shard-00-01-jxeqq.mongodb.net:27017,cluster0-shard-00-02-jxeqq.mongodb.net:27017/100YWheatherSmall?replicaSet=Cluster0-shard-0" --authenticationDatabase admin --ssl --username m001-student --password m001-mongodb-basics```

 	```mongo "mongodb://wikidb-yb1gv.mongodb.net:27017?replicaSet=Cluster0-shard-0" --authenticationDatabase admin --ssl --username m001-student --password m001-mongodb-basics```

 * <strong>SHOW COLLECTIONS</strong>:
   ```show collections``` - Exibe as coleções disponíveis.

 * <strong>USE</strong>:
  ```use movies ``` - Seleciona a db movies para uso.

 * <strong>SHOW DBS</strong>:
  ```show dbs``` - Exibi as bases de dados criadas.

 * <strong>LOAD FILE</strong>
 ```load("loadMovieDetailsDataset.js")``` - Executa o script em loadMovieDetailsDataset.js("Arquivo com script que importa os dados.")

 * <strong>SHOW DATA IN COLLECTION </strong>
 ```db.collection.find().pretty()``` - Exibi todos os dados da coleção.

 * <strong> INSERT ONE DOCUMENT </strong>
 ```db.movieScrath.insertOne({title:"Star{Trek II: The Wrath of Khan", year: 1982, imdb: "tt0084726"})``` - Inserindo um documento na coleção.

 * <strong> INSERT MANY DOCUMENTS </strong>
	``` 
	 	db.moviesScratch.insertMany(
	    [
	        {
		    "_id" : "tt0084726",
		    "title" : "Star Trek II: The Wrath of Khan",
		    "year" : 1982,
		    "type" : "movie"
	        },
	        {
		    "_id" : "tt0796366",
		    "title" : "Star Trek",
		    "year" : 2009,
		    "type" : "movie"
	        },
	        {
		    "_id" : "tt0084726",
		    "title" : "Star Trek II: The Wrath of Khan",
		    "year" : 1982,
		    "type" : "movie"
	        },
	        {
		    "_id" : "tt1408101",
		    "title" : "Star Trek Into Darkness",
		    "year" : 2013,
		    "type" : "movie"
	        },
	        {
		    "_id" : "tt0117731",
		    "title" : "Star Trek: First Contact",
		    "year" : 1996,
		    "type" : "movie"
	        }
	    ],
	    {
	        "ordered": false 
	    }
		);
	``` - Inserindo vários documentos juntos não ordenados. 

 * <strong></strong>
	 db.movieDetails.find({'rated':'PG', 'awards.nominations':10}).count()
	 Cursor is IT
	 db.movieDetails.find({'genres':'Western'},{'title':1,'_id':0}).limit(1)
	 db.movieDetails.updateOne({
	  title: "The Martian"
	 }, {
	   $set: {
	     poster: "www.google.com.br"
	    }
	 })

[Update Operators]<https://docs.mongodb.com/manual/reference/operator/update/>
db.movieDetails.updateMany({
	rated: null
	}, {
	$unset: {
		rated: ""
	}
	})

deleteOne()
deleteMany()



db.movieDetails.find({runtime: {$gt:90}}, {_id: 0, title:1,runtime: 1})
db.movieDetails.find({runtime: {$gt:90, $lt: 120}}, {_id: 0, title:1,runtime: 1})
db.movieDetails.find({runtime: {$gte:180},"tomato.meter":{$gte : 95}}, {_id: 0, title:1,runtime: 1})
db.movieDetails.find({rated: {$ne:"UNRATED"}}, {_id: 0, title:1,runtime: 1})
db.movieDetails.find({rated: {$in:["G","PG"]}}, {_id: 0, title:1,runtime: 1})
[Query Operators]<https://docs.mongodb.com/manual/reference/operator/query/>
$gt, $gte, $lt, $lte,$eq,$ne,$in,$nin
[Query type]<https://docs.mongodb.com/manual/reference/operator/query/type/>
db.movieDetails.find({"tomato.rating":{$type:"double"}}).count()
db.data.find({atmosphericPressureChange:{$exists:false}}).count()
db.movieDetails.find({$or: [{"tomato.meter":{$gt: 95}},{"metacritic":{$gt:88}}]},
					 {_id:0,title: 1, "tomato.meter":1, "metacritic":1})

db.shipwrecks.find({$or[{"watlev":{$eq:"always dry"}},{"depth":{$eq:0}}]})

db.movieDetails.find({$and: [{"tomato.meter":{$gt: 95}},{"metacritic":{$gt:88}}]},{_id:0,title: 1, "tomato.meter":1, "metacritic":1})
	== EQ == 
db.movieDetails.find({"tomato.meter":{$gt: 95},"metacritic":{$gt:88}},{_id:0,title: 1, "tomato.meter":1, "metacritic":1})

db.movieDetails.find({$and: [{"metacritic":{$ne: null}},{"metacritic":{$exists:true}}]},{_id:0,title: 1, "tomato.meter":1, "metacritic":1})

db.movieDetails.find({"genres":{$all: ["Comedy","Drama","Romance"]}})
db.movieDetails.find({countries:{$size:1}}).pretty()
db.surveys.find({results:{$elemMatch:{product:"abc",score:7}}}).count()

db.movieDetails.find({"awards.text":{$regex: /^Won .*/}},{_id:0,title:1,"awards.text":1}).pretty()