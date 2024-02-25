Open the project in VScode

`code .`

Review the following files:
```
./src/main/java/com/example/QuoteController.java
application.yaml
schema.graphqls
```

Boot the application:
`mvn spring-boot:run`

Open the application:

http://localhost:8080

Show the GraphQL representation of the app:

http://localhost:8080/graphiql

Run some queries:

query {  
  allAuthors {
      name
      wikipediaUrl
      field
  }
}

{
  randomQuote {
    id,
    quote,
    author {
      name
      wikipediaUrl
      field
    }
  }
}

mutation {
    addAuthor(id:6, name:"Aristotle", field:POLITICS,wikipediaUrl:"https://en.wikipedia.org/wiki/Aristotle") {
        name
        wikipediaUrl
        field
    }
}

query {
    allAuthors {
        name
        wikipediaUrl
        field
    }
}
