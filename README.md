# GraphQL-learnings
My journey towards learning this new technology. i.e GraphQL

### What is GraphQL?

GraphQL is a declrative data fetching language. It means that what is requested in request, the server sends only that information and no extra stuff with it in response.

It saves many round-trips to server for getting the enough data to show to the user.

Unlike REST we can fetch all the required information in one request instead of sending the multiple requests to the server.

### Who created it?
Facebook, started using it in their native app in 2012

Open sourced in 2015 and now community of devs all around the world is maintaining the graphql.

### Overview of how it works as compared to REST
Let's say we are making an app for showing movie details, our rest endpoints might look like the following:

```bash
# route to get list of all movies
/api/movies

# route to get a single movie info
/api/movies/id

# get actors of movie
/api/movies/id/actors

# get director(s) of movie
/api/movies/id/directors

# get movies in which the actor has acted in
/api/actors/id/movies

.
.
.
# The list goes on...
```

That is a lot of work for server!

#### What if we want just the names of actors and directors and not all of their info?
> Manually handle this scenario! ☹️

#### What if we want just the title of movies and names of actors associated with it?
> Manually handle this scenario! ☹️

### GraphQL is here to solve this problem...

### How many end-point are required?
> Only 1 :tada:

### Send the request to end-point specifying what you need and server will respond with the data that you need.

## GraphQL Schema Definition Language (SDL)

### Types
You can refer them as table definition or schema/relation etc
```
type Actor {
    id: ID!
    name: String!
    date_of_birth: Date!
    movies: [Movie!]!
}

type Director {
    id: ID!
    name: String!
    date_of_birth: Date!
    movies: [Movie!]!
}

type Movie {
    id: ID!
    title: String!
    released: Date!
    actors: [Actor!]! // 1:M Relation
    directors: [Director!]! // 1:M Relation
}
```

Now we can fetch the data with Query
Here, we use GraphQL Query according to the schema designed on the GraphQL server
```
// we want to get all movies with their title, actors names and directors names
{
    allMovies {
        title,
        actors {
            name
        },
        directors {
            name
        }
    }
}
```
The result will be the JSON object with all the required data fields:
```json
{
    "allMovies": [
        {
            "title": "The Matrix",
            "actors": [
                {
                    "name": "Keanu Reevs"
                },
                // and other actors as well
            ],
            "directors": [
                {
                    "name": "XYZ Director"
                }
            ]
        }
    ]
}
```
