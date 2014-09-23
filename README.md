
# Find movies and add them to our database
```

/************************************************
/*
/* Find movies using multiple search and filter strategies
/*
/************************************************

$builder=Finder/Builder::create();

$builder->addSearchStrategy(new Search\LatestMovies(), 5);
$builder->addSearchStrategy(new Search\BoxOfficeMovies(), 4);
$builder->addSearchStrategy(new Search\PopularMovies(), 3);
$builder->addSearchStrategy(new Search\ComedyMovies(), 2);
$builder->addSearchStrategy(new Search\HorrorMovies(), 1);

$builder->addFilterStrategy(new Filter\RemoveDuplicatesFrom());

$finder=Finder::build();

try{

    $movies=$finder->find();

}
catch(MoviesNotFoundException $e){

     $this->raise(new MoviesNotFoundEvent());

}


/************************************************
/*
/* Add new found movies to our database
/*
/************************************************

$builder=new Database\Builder::create();
$builder->setReplacePolicy(false);
$db=$builder::buildDatabase();
$db->addCollecion($movies);

```
