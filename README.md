# Counter Example

This is an example of a simple smart contract and how to deploy it to our devnet. The example is the counter smart contract.

# Usage

## Step 1 - Compile smart contracts.
```bash
$ cargo build --release
```

## Step 2 - Update keys.
In `keys` directory you can find example keys. They might not have sufficient funds, so please create you own keys using [Clarity](http://clarity.casperlabs.io). Remember to fund your keys using Clarity's faucet. 

## Step 3 - Deploy the counter smart contract.
Make sure to run scripts in the root directory!
```bash
$ ./scripts/deploy-smart-contract.sh
```

## Step 4 - Check the counter value.
```bash
$ ./scripts/check-counter.sh
```
Value of the counter should be `0`.

## Step 5 - Increment the counter.
```bash
$ ./scripts/increment-counter.sh
```

Now check the value of the counter again. It should be `1`.

## GraphQL
You can check the value of the counter using devnet's GraphQL console:
https://devnet-graphql.casperlabs.io

Go to the GraphQL console and then:

### Check latest block hash in 
```
query {
  dagSlice(depth: 1) {
      blockHash
  }
}
```

### Get public key of your account
```bash
$ cat keys/public-key
```

### Check the counter value.
Put block hash under `blockHashBase16Prefix` and your public key under `keyBase`.
```
query {
  globalState(
    blockHashBase16Prefix: "96720f16a215b5e55f1a7475256370f48efa932248b7bcd633d29413a5c1f033"
    StateQueries: [
      {
        keyType: Address
        keyBase16: "64d0c86f888e925731cae4398c6ea86d26a14e2574e70b36bd4eeaec3a292cde"
        pathSegments: ["counter", "count"]
      }
    ]
  ) {
    value {
      __typename
      ... on I32 {
        int: value
      }
    }
  }
}
```
