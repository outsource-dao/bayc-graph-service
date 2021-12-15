# Bored Ape Yacht Club Graph Service

### Queries

#### Basic query

```graphql
{
  tokens {
    id
    tokenID
    contentURI
    collection
    eyes
    background
    hat
    mouth
    clothes
    fur
    earring
  }
}
```

#### Full Text Search

```sh
{
  tokenSearch (text: "Orange") {
    id
    tokenID
    contentURI
    collection
    eyes
    background
    hat
    mouth
    clothes
    fur
    earring
  }
}
```

#### Filtering

```sh
{
  tokens(
    where: {
      collection: "Mutant Ape Yacht Club"
    }
  ) {
    id
    tokenID
    contentURI
    collection
    eyes
    background
    hat
    mouth
    clothes
    fur
    earring
  }
}
```

#### Query tokens by owner

```graphql
{
  tokens(
    where: {
      owner: "0x9056d15c49b19df52ffad1e6c11627f035c0c960"
    }
  ) {
    id
    tokenID
    contentURI
    collection
    eyes
    background
    hat
    mouth
    clothes
    fur
    earring
  }
}
```

#### Relational data (tokens and owners)

```graphql
{
  tokens {
    id
    tokenID
    contentURI
    collection
    eyes
    background
    hat
    mouth
    clothes
    fur
    earring
    owner {
      id
      tokens {
        id
      }
    }
  }
}
```

#### Change order direction

```graphql
{
  tokens(
    orderBy: updatedAtTimestamp
    orderDirection: desc
  ) {
    id
    tokenID
    contentURI
    collection
    eyes
    background
    hat
    mouth
    clothes
    fur
    earring
  }
}
```


### Working with IPFS in a subgraph

This project can also serve as a useful reference for how to query IPFS from within a subgraph mapping template, using methods like `ipfs.cat` from the [`graph-ts`](https://github.com/graphprotocol/graph-ts) library and how to manage the data once it comes back from IPFS:

```javascript
let data = ipfs.cat(ipfshash)

let value = json.fromBytes(data!).toObject()

let attributes = value.get('attributes').toArray()

for (let i = 0; i < attributes.length; i++) {
  let item = attributes[i].toObject()
  // do stuff
}
```