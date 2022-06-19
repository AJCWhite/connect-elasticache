
**connect-elasticache-redis** provides Redis session storage for Express exapnding on **connect-redis** for support for multiple or global elasticache read replicas

## Installation

npm:

```sh
npm install redis connect-elasticache-redis express-session
```


## API

```js
const session = require("express-session")
let RedisStore = require("connect-redis")(session)

// redis@v4
const { createClient } = require("redis")
// master
let redisMasterClient = createClient({ legacyMode: true })
redisMasterClient.connect().catch(console.error)
// replica
let redisReplicaClient = createClient({ legacyMode: true })
redisReplicaClient.connect().catch(console.error)

// redis@v3
const { createClient } = require("redis")
// master
let redisMasterClient = createClient()
// replica
let redisReplicaClient = createClient()


app.use(
  session({
    store: new RedisStore({ clientMaster: redisMasterClient, clientReplica: redisReplicaClient }),
    saveUninitialized: false,
    secret: "keyboard cat",
    resave: false,
  })
)
```

**All credit goes to** https://www.npmjs.com/package/connect-redis