# Installation

**Step1**: Add nem-library dependency to `package.json`

```sh
$> npm install nem-library --save
```

**Step2**: Setup phase

In your application startup file, initialize NEMLibrary.
 
```typescript
import { NEMLibrary, NetworkTypes } from "nem-library";

NEMLibrary.bootstrap(NetworkTypes.TEST_NET);
```

Your application can have two modes, `NetworkTypes.TEST_NET` and `NetworkTypes.MAIN_NET`.
Depending on the environment that you want to use, you should call the bootstrap method, with `MAIN_NET`
or `TEST_NET`.

Because the application should have a unique environment, calling `NEMLibrary.bootstrap(_)` multiple times will throw an `Error`.
In case you need to change between environments in runtime, call `NEMLibrary.reset()` first.

# Configure endpoints

Each infrastructure endpoints share the same constructor.
 
```typescript
// Using custom NIS Node
const accountHttp = new AccountHttp([{
    protocol: "http",
    domain: "104.128.226.60",
    port: 7890
}]);

// Using default NIS Node
const accountHttpWithDefaultConfig = new AccountHttp();
```

The default values are:

**TEST NET**

| Parameter | Value |
| ---       | ---   |
| protocol  | http    |
| domain    | bigalice2.nem.ninja |
| port      | 7890 |

| Parameter | Value |
| ---       | ---   |
| protocol  | https    |
| domain    |pretestnet1.nem.ninja |
| port      | 7778 |

**MAIN NET**

| Parameter | Value |
| ---       | ---   |
| protocol  | http    |
| domain    | alice6.nem.ninja |
| port      | 7890 |


| Parameter | Value |
| ---       | ---   |
| protocol  | https    |
| domain    | nis2.wnsl.biz |
| port      | 7779 |
