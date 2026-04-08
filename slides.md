---
title: Lets talk about ... GraphQL
---

---
build: true

## Lets Talk about...
# GraphQL

---

# What is GraphQL?

---
build: true

## What is GraphQL?
- Invented by Facebook Mobile Department (2012)
- Open Sourced 2015
- Query Language
- Made for APIs

---

# API?

---
background: assets/images/philosoraptor.jpg

## Why don't use
# REST

---
build: true

## Whats wrong with REST?
- Multiple calls
- Define nesting
- Define selected fields
- Multiple endpoints
- GET requests with limited query size

---

# All in one Query?

---
background: assets/images/philosoraptor.jpg

## Why don't use
# SQL

---
build: true

## Whats wrong with SQL?
- Database dependent
- Only subset of features
- Confusing notation
- Not made for API

---
background: assets/images/fry.jpg

# Why GraphQL?

---
build: true

## Why GraphQL?
- De-Coupled from storage
- Whole request in one query
- POST to a single endpoint
- Validated and Structured
- Easy to optimize

---
background: assets/images/crash.jpg
cover: true

# &nbsp;
# Crash Course

---

# Server

---

# Types

---

```graphql linenums
type Employment {
  firstName: String!
  lastName: String!
  worksAt: [Shift]!
}
```
- &nbsp;
- &nbsp;
- &nbsp;

---

```graphql linenums h0
type Employment {
  firstName: String!
  lastName: String!
  worksAt: [Shift]!
}
```
- **Employment**
- *GraphQL Object Type*, meaning it's a type with some fields.
- Most of the types in your schema will be object types.

---

```graphql linenums h1-3
type Employment {
  firstName: String!
  lastName: String!
  worksAt: [Shift]!
}
```
- **firstName, lastName, worksAt**
- *Fields* on *Employment* Type. That are the only
- fields which can appear on a Employment type.

---

```graphql linenums h1
type Employment {
  firstName: String!
  lastName: String!
  worksAt: [Shift]!
}
```
- **String**
- Build in *Scalar Type* - resolve to a single scalar
- without any sub selections.

---

```graphql linenums h1
type Employment {
  firstName: String!
  lastName: String!
  worksAt: [Shift]!
}
```
- **String!**
- *Non-nullable* field.
- &nbsp;

---

```graphql linenums h3
type Employment {
  firstName: String!
  lastName: String!
  worksAt: [Shift]!
}
```
- **[Shift]!**
- *Array* of shifts. Since its also *non-nullable*, you
- can always expect an array (with zero or more Shifts).

---

# Scalars

---

## Build in Scalars
- *Int*: Signed 32-bit Integer.
- *Float*: Signed double-precision floating-point value.
- *String*: A UTF-8 character sequence.
- *Boolean*: *true* or *false*
- *ID*: Unique Identifier serialized same way as String

---

## Custom Scalars
- ```graphql
  scalar Date
  ```

---

## Enums
- ```graphql
  enum Style {
    NONE
    BOLD
    ITALIC
    UNDERLINE
  }
  ```

---

## Interface
- ```graphql
  interface Person {
    firstName: String!
    lastName: String!
  }
  ```

---

## Using Interface
- ```graphql
  type Employment implements Person {
    firstName: String!
    lastName: String!
    worksAt: [Shift]!
  }
  ```

---

## Union
- ```graphql
  union Conflict =
    Shift | Absence | HourAccount
  ```

---

## Arguments
- ```graphql linenums h3
  type Employment {
    firstName: String!
    lastName: String!
    worksAt: [Shift]!
  }
  ```

---

## Arguments
- ```graphql linenums h4-5
  type Employment {
    firstName: String!
    lastName: String!
    worksAt(
      startsAt: Date,
      endsAt: Date
    ): [Shift]!
  }
  ```

---

# Schema

---
background: assets/images/gql-model.svg

&nbsp;

---

```graphql
schema {
  query: Query
  mutation: Mutation
}
```

---

```graphql
... scalars ...
... interfaces ...
... unions ...
... types ...

schema {
  query: Query
  mutation: Mutation
}
```

---

## Query
- ```graphql
  type Query {
    employment(id: ID): Employment
  }
  ```

---

## Query
- ```graphql
  type Query {
    employment(id: ID): Employment
    employments(
      id: ID,
      firstName: string
    ): [Employment]!
  }
  ```

---

## Query
- ```graphql
  type Query {
    employment(id: ID): Employment
    employments(
      ids: [ID],
      firstName: string
    ): [Employment]!
    billingTypes: [BillingType]!
  }
  ```

---

## Mutation
- ```graphql
  type Mutation {
    createEmployment(
      userId: ID!,
      companyId: ID!,
      firstName: String!,
      lastName: String!
    ): Employment!
  }
  ```

---

## Input Type
- ```graphql
  input EmploymentInput {
    firstName: String!
    lastName: String!
  }
  ```

---

## Mutation
- ```graphql
  type Mutation {
    createEmployment(
      userId: ID!,
      companyId: ID!,
      fields: EmploymentFields!,
    ): Employment!
  }
  ```

---

# Client

---

# Call Queries

---

## Basic

```graphql
{
  employment(id: 1) {
    firstName
  }
}
```

---

## Result

```json
{
  "employment": {
    "firstName": "Tamino"
  }
}
```

---

## Named

```graphql
query FetchEmployment {
  employment(id: 1) {
    firstName
  }
}
```

---

## With Parameters

```graphql
query FetchEmployment($id: Int!) {
  employment(id: $id) {
    firstName
  }
}
```

---

## Query Call

```js
gql`
  query FetchEmployment($id: Int!) {
    employment(id: $id) {
      firstName
    }
  }
`, {
  id: 1,
}
```

---

## Call Mutations
- ```graphql
  mutation CreateEmployment(
    $userId: Int!,
    $companyId: Int!,
    $firstName: String!,
  ) {
    createEmployment(userId: $userId, ...) {
      id
    }
  }
  ```

---

- # [Demo](https://launchpad.graphql.com/10vn1745k9)
- ![](assets/images/like-a-boss.jpg)

---

# [Libraries](http://graphql.org/code/)

---
type: section

# Apollo

---
build: true

## What is Apollo?
- GraphQL with benefits
- A couple of packages

---
build: true

- ## Server
  ![](assets/images/apollo-server.svg)
  - Lambda
  - EC2
  - Express

---
build: true

- ## Engine
  ![](assets/images/apollo-engine.svg)
  - Tracking
  - Monitoring
  - Caching

---
build: true

- ## Client
  ![](assets/images/apollo-client.svg)
  - Transfer
  - Binding
  - Reactivity

---

# Reactivity?

---
background: assets/images/gql-model.svg

&nbsp;

---
background: assets/images/gql-events.svg

&nbsp;

---
background: assets/images/gql-subscriptions.svg

&nbsp;

---

<video src="assets/videos/communication.mov" loop controls></video>

---
background: assets/images/apollo-trace.png

&nbsp;

---
background: assets/images/apollo-caching-trace.png

&nbsp;

---
background: assets/images/apollo-errors.png

&nbsp;

---
background: assets/images/apollo-schema.png

&nbsp;

---
background: assets/images/apollo-trends.png

&nbsp;

---

- # [Demo](https://engine.apollographql.com/service/launchpad-10vn1745k9)
- ![](assets/images/like-a-boss.jpg)

---
background: assets/images/all-the-things.jpg

# &nbsp;
# Thats it

---

## Whats next?
- [Apollo](https://www.apollographql.com/)
- [GraphQL](http://graphql.org/)
- [Playground](http://launchpad.graphql.com)
- [Slides](https://tamino-martinius.github.io/lets-talk-about--graphql)

---
type: section

# Questions?
