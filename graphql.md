# GraphQL with Java 
GrapQL - simple reference - https://www.howtographql.com


## Concepts
### TYPES
Using Schema Definition Language  for defining types
<pre>
type Person {
    name :String!
    age: Int!
    post: [Post!]
}

type Post {
    title :String!
}
</pre>
! : indicates this field is required

[ ] : indicates the list

### SCHEMA
Most types in your schema will just be normal object types, but below types that are special within a schema:
<pre>
schema {
  query: Query
  mutation: Mutation
  subscription: Subscription // for streams  
}
</pre>

### Invoking the Query
This would contain as follows
- Root fields 
- Resolvers 

#### Root Fields
<pre>
query{
    human{
        name
        age
    }

}
</pre>
#### Resolvers
For the schema mentioned below
<pre> 
type Link {
  url: String!
  description: String!
}

type Query {
  allLinks: [Link]
}
</pre>

Resolvers in Java would be as follows
<pre>
public class Query implements GraphQLRootResolver {
    
    private final LinkRepository linkRepository;

    public Query(LinkRepository linkRepository) {
        this.linkRepository = linkRepository;
    }

    public List<Link> allLinks() {
        return linkRepository.getAllLinks();
    }
}
</pre>


### Basic POM dependencies for graphQL
<pre>
    <dependency>
        <groupId>com.graphql-java</groupId>
        <artifactId>graphql-java</artifactId>
        <version>3.0.0</version>
    </dependency>
    <dependency>
        <groupId>com.graphql-java</groupId>
        <artifactId>graphql-java-tools</artifactId>
        <version>3.2.0</version>
    </dependency>
    <dependency>
        <groupId>com.graphql-java</groupId>
        <artifactId>graphql-java-servlet</artifactId>
        <version>4.0.0</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.0.1</version>
        <scope>provided</scope>
    </dependency>
</pre>

# Docker Image of Mongo

## Downloaded the docker image of mongo
<pre>
docker pull mongo
</pre>
we can also specify a particular version, in that case just add the version as follows
<pre> docker pull mongo:2.3.4</pre>

## Start the container of mongo

Command would be as follows

docker run --name [NAME_OF_CONTAINER] mongo -p [INTERNAL_PORT]:[EXTERNAL_PORT]  -d

-d : detach mode
--name : name of the container 

<pre>
docker run  -d -p 27017-27019:27017-27019 --name mongodb mongo
</pre>

## Create DB 
we can execute inside the container with following command
<pre>
docker exec -it mongodb bash
</pre>

-it : interactive mode
mongodb: name of the container
bash: type of shell 