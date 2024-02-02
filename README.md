> :warning: This repository was archived automatically since no ownership was defined :warning:
>
> For details on how to claim stewardship of this repository see:
>
> [How to configure a service in OpsLevel](https://www.notion.so/pleo/How-to-configure-a-service-in-OpsLevel-f6483fcb4fdd4dcc9fc32b7dfe14c262)
>
> To learn more about the automatic process for stewardship which archived this repository see:
>
> [Automatic process for stewardship](https://www.notion.so/pleo/Automatic-process-for-stewardship-43d9def9bc9a4010aba27144ef31e0f2)

# NodeJS Configuration Manager

## Install

`yarn add @pleo-io/config-man`

## Initialize

Add `[ProjectRoot]/config-man.json` file

```json
{
    "schema": [{"key": "server.port", "type": "number", "default": 8080, "nullable": false}]
}
```

```ts
import * as configMan from '@pleo-io/config-man'

configMan.init({
    cwd: __dirname,
    removeUnknown: true,
    configs: [
        {type: configMan.ConfigType.DEFAULT},
        {type: configMan.ConfigType.DYNAMODB, tableName: 'Configuration-Table', region: 'eu-west-1'},
        {type: configMan.ConfigType.JAVASCRIPT, filepath: path.resolve('config.js')},
        {type: configMan.ConfigType.JSON, filepath: path.resolve('config.json')},
        {type: configMan.ConfigType.ARG, prefix: 'CM_'},
        {type: configMan.ConfigType.ENV, prefix: 'CM_},
    ]
});

async function startApp() {
    // Wait for config to be ready
    await configMan.ready;

    const port = configMan.get('server.port');
    // etc...
}
```
