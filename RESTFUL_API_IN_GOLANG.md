### Introduction to
# RESTFUL API IN GOLANG



#### OVERVIEW

These are the notes for a demo in which the concepts of REST applied to an API are briefly explained, with examples in Golang. Also, it includes problems that may arise, particularly with this language, and some options on how to solve them.


#### INDEX

- [Intro to RESTful API](#intro-to-restful-api)
  - [What is an API?](#what-is-an-api?)
  - [What is REST?](#what-is-rest?)
  - [So, what is a RESTful API?](#so-what-is-a-restful-api?)
  - [Resources](#resources)
- [Golang examples and tools](#golang-examples-and-tools)
  - [Basic example](#basic-example)
  - [Util libraries](#util-libraries)
  - [Other examples and resources](#other-examples-and-resources)
  - [Other tools for bigger services](#other-tools-for-bigger-projects)


#### INTRO TO RESTFUL API

##### What is an API?

API stands for Application Programming Interface. So, it is an interface (or communication protocol) between a client and a server. Specifically, it is a user interface to data and systems that is consumed by applications rather than humans. 

##### What is REST?

REST stands for REpresentational State Transfer. It is a software architectural style that consists of six constraints.
It was first presented by Roy Fielding in 2000 in his PhD dissertation.

**Client-server architecture**

This principle is related to the separation of concerns. It improves scalability and independence.

**Stateless**

The server does not memorize the previous requests (it is stateless). Each request must contain all the information necessary to service the request, and the session state is held in the client.

**Cacheable**

Clients and intermediaries can cache responses. Responses must therefore, implicitly or explicitly, define themselves as cacheable or not.

**Uniform interface**

The purpose is to transmit information in a standardized way. So there must be uniformity in resources (how entities are represented), representations (in what format), descriptive messages (what is the intention of the method or resource) and the HATEOAS principle (Hypermedia as the engine of application state, that means client should then be able to use server-provided links dynamically to discover all the available actions and resources it needs).

**Layered system**

A client cannot ordinarily tell whether it is connected directly to the end server, or to an intermediary along the way. So this principle aims to the decoupling.

**Code on demand (optional)**

Servers can temporarily extend or customize the functionality of a client by transferring executable code.


##### So, what is a RESTful API?

Exercise: with this information now you can write your own definition.


##### Resources 

- `https://everipedia.org/wiki/lang_en/Application_programming_interface`
- `https://www.mulesoft.com/resources/api/what-is-an-api`
- `https://www.freecodecamp.org/news/what-is-an-api-in-english-please-b880a3214a82/`
- `https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm`
- `https://restfulapi.net/`
- `https://everipedia.org/wiki/lang_en/Representational_state_transfer`
- UDEMY COURSE: REST API Design, Development & Management: `https://www.udemy.com/course/rest-api/learn/lecture/4807280#overview`


#### GOLANG EXAMPLES


##### Basic example

- Repo: `https://github.com/DizNicolasAmor/go-simple-api`
- Description: in this repo we have a service that manages a collection of “persons” entities.
- Exercises:
  - Download and open the repo. Look at the scaffolding and try to understand the general flux. Explain it briefly (2 min).
  - Return to the repo and now pay attention to the libraries it implements. Propose a brief explanation of what each is in charge of.

##### Util libraries

**net/http**

- Native golang package that provides HTTP client and server implementations.
- Doc: `https://golang.org/pkg/net/http/`

**net/http/httptest**

- Native golang package to test http requests.
- Doc: `https://golang.org/pkg/net/http/httptest/`
- Example: `https://golang.org/src/net/http/httptest/example_test.go`

**encoding/json**

- Native golang package that implements encoding and decoding of JSON. In other words, it handles the mapping between JSON and Go values.
- Doc: `https://golang.org/pkg/encoding/json/`

**mux**

- It is a  URL router and dispatcher. We use this package to match URL paths with their handlers and with HTTP verbs.
- Doc: `https://github.com/gorilla/mux`
- Example: 
	```
	func main() {
		r := mux.NewRouter()
		r.HandleFunc("/", HomeHandler).Methods("GET")
		r.HandleFunc("/products", ProductsHandler).Methods("GET")
		r.HandleFunc("/articles", ArticlesHandler).Methods("GET")
		http.Handle("/", r)
	}
	````

**bson**

- It means binary json. I use this package to create and manage IDs. It is related to mongo, but you can use it regardless of this DB. For example, in the previous repo there is no DB and I hardcoded the data in a local variable.
- Source: `https://gopkg.in/mgo.v2/bson`
- Doc: `https://godoc.org/gopkg.in/mgo.v2/bson`
- Usage: first generate a swagger.json or swagger.yaml and then serve it, either locally or in any online swagger viewer.

**validator**

- It validates values in golang structs and primitive types based on tags.
- Source: `https://gopkg.in/go-playground/validator.v9`
- Doc: `https://godoc.org/gopkg.in/go-playground/validator.v9`

**go-swagger**

- It is a tool to document your APIs.
- Doc: `https://github.com/go-swagger/go-swagger`
- Usage: first generate a `swagger.json` or `swagger.yaml` and then serve it, either locally or in any online swagger viewer.


##### Other examples and resources

- Full stack application (a Restaurant App Demo) with two Golang APIs orchestrated with a mongo DB and consumed from two frontend services: `https://github.com/DizNicolasAmor/restaurant-app`
- A TODO list built with Golang: `https://github.com/westonplatter/example-golang-todo/blob/master/server.go`
- Go REST API for managing blog posts: `https://github.com/Duncanian/go-rest-api`
- Go REST API tutorial article: `https://dev.to/moficodes/build-your-first-rest-api-with-go-2gcj`
- Medium article “Build a RESTful JSON API with Golang”: `https://medium.com/the-andela-way/build-a-restful-json-api-with-golang-85a83420c9da`
- Medium article “Build and deploy a secure REST API with Go, postgresql and Gorm”: `https://medium.com/@adigunhammedolalekan/build-and-deploy-a-secure-rest-api-with-go-postgresql-jwt-and-gorm-6fadf3da505b`
- UDEMY course: “GetGoing: Introduction to Golang”. Instructor: Angad Sharma. From Chapter 4(“Section 4: Introduction to API development with Go”) on: `https://www.udemy.com/course/getgoing/learn/lecture/15679926`


##### Other tools for bigger services

The first Golang real world project I participated was this: `https://gitlab.com/fast-dev-view`
Maybe if you have access you can read it. But if not, don’t worry, I just want to mention other tools that you probably will use when your service gets bigger.

**Connection with DB**

Probably you will need to use packages to connect to a DB service. In this example there is a connection with a postgresql DB service and there is also the util GORM framework.

**Sub-routes with mux**

With the mux package we can also order and clarify our routes with sub-routes.

**reflect**

This Golang native package manipulates data with arbitrary types. I used it when I needed to save values from a var with a struct type, into a var with a different struct type. Doc: `https://golang.org/pkg/reflect/`

**sync**

This Golang native package provides basic synchronization. I used it when in a handler I had to consume data from different services and integrate them: for example, wait for different goroutines and work with resulting data. Doc: `https://golang.org/pkg/sync/`
