# gqlmerge

A tool to merge and stitch modularized GraphQL files into one schema file

## Stack

- Built in Go
- No 3rd party dependency

## Features

- Fast, blasing fast
- Find `*.graphql` and `*.gql` files in recursive way
- CLI to use in shell or script

## How to use

### Install to use in CLI

Homebrew

```shell
$ brew install mattdamon108/tools/gqlmerge
```

Using `go get`

```shell
$ go get -u github.com/mattdamon108/gqlmerge
```

Building with source code

```shell
$ git clone https://github.com/mattdamon108/gqlmerge

$ cd gqlmerge

$ go install
```

### Use as a go module

Import gqlmerge module

```go
import gql "github.com/mattdamon108/gqlmerge/lib"

func main(){
	// ...

	// path should be a relative path
	schema := gql.Merge(path)
}
```

## What for?

If you have a modularized GraphQL schema files, such as `*.graphql`, there might be a duplicated types among them. In this case, `gqlmerge` will help you to merge and stitch it into one schema.

_Before_

```graphql
# GetMyProfile.graphql

type Query {
  getMyProfile: UserResponse!
}

type UserResponse {
  ok: Boolean!
  error: String
  user: User
}

type User {
  id: ID!
  email: String!
  fullName: String!
  # ...
}

# CheckIfExists.graphql

type Query {
  checkIfExists(userId: ID!): CheckIfExistsResponse!
}

type CheckIfExistsResponse {
  ok: Boolean!
  error: String
  user: [User]!
}

type User {
  id: ID!
  email: String!
  fullName: String!
  # ...
}
```

_Merge & Stitch_

```shell
$ gqlmerge ./schema schema.graphql
```

_After_

```graphql
type Query {
  getMyProfile: UserResponse!
  checkIfExists(userId: ID!): CheckIfExistsResponse!
}

type UserResponse {
  ok: Boolean!
  error: String
  user: User
}

type CheckIfExistsResponse {
  ok: Boolean!
  error: String
  user: [User]!
}

type User {
  id: ID!
  email: String!
  fullName: String!
  # ...
}
```

## How to use

```shell
$ gqlmerge [PATH] [OUTPUT]

// PATH : directory path of *.graphql or *.gql
// OUTPUT : output file name
```

## Next to do

- [ ] additional error handling
