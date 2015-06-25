#Scala command utilities

This library provides utilities that help create more readable code. It does this by providing an abstraction that makes dealing with types easier.

```scala
def update(id: String) = Commands { request =>
  for {
    _    <- getUserById(id) ifNone Return(NotFound)
    json <- jsonFromRequest(request) ifNone Return(BadRequest("invalid json"))
    user <- jsonToUser(json) ifLeft Return(validationProblemToJson)
    _    <- saveUser(user)
  } yield NoContent
}
```

In our development work we found we often have to wire together functions that return a variaty of types that are most of the time not directly compatible. For example:

- `Future[A]`
- `Future[Option[A]]`
- `A`
- `Option[A]`
- `Future[Either[A, B]]`

This library makes working with results like these easier.

This library consists of two parts:

1. `core` The main machinery
2. `play` A specialized version for the Play Framework


##Installation

``` scala
libraryDependencies += "net.kaliber" %% "scala-command-utilities-core" % "0.1"
// if you are using play use the following (you can skip the core as it's automatically loaded)
libraryDependencies += "net.kaliber" %% "scala-command-utilities-play" % "0.1"

resolvers += "Rhinofly Repository" at "http://maven-repository.rhinofly.net:8081/artifactory/libs-release-local"
```

##Usage

Please refer to the documentation directories in the `core` and `play` directories.
