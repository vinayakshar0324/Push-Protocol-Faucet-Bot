## Push-Protocol-Faucet-Bot

Simple Discord Bot that allows token faucet chatbot for Push Protocol that distributes test tokens ($PUSH) to specified addresses. This innovative feature will allow users to interact with the chatbot, receive test tokens, and experience the power of Push Protocol firsthand.

## Command Structure

The Discord bot accepts a command that looks like this:

`/faucet <network> <token> <address>` and then disburse a predefined amount of funds (specific to that token on that network) to the address sent.


## Supported networks

Currently, the following networks are supported by default:

-   Ethereum Goerli (ETH)

Anyways, it is possible to add any token of any network (EVM) by using the following interface:

```typescript
interface Networks {
    [network: string]: {
        chainId: number;
        tokens: {
            [token: string]: {
                amount: number; // @notice that this amount is measured in ETH
                address?: string;
                isNativeToken?: boolean;
            };
        };
        blockExplorer: string;
    };
}
```

## Features

### Faucet:

-   People can request tokens via the `/faucet <network> <token> <address>` command.
-   Validations with warning/error messages.
-   requesting tokens (based on Discord User ID).
-   Easy to add/remove networks and tokens.

### Developer Friendly:

-   Written with TypeScript.
-   Uses the [discord.js](https://discord.js.org/) framework.

## Setup

1. Copy example config files.
    - Navigate to the `config` folder of this project.
    - Copy the `config.example.json` as `config.json`.
2. Obtain a bot token.
    - You'll need to create a new bot in your [Discord Developer Portal](https://discord.com/developers/applications/).
        - See [here](https://www.writebots.com/discord-bot-token/) for detailed instructions.
        - At the end you should have a **bot token**.
3. Modify the config file.
    - Open the `config/config.json` file.
    - You'll need to edit the following values:
        - `client.id` - Your discord bot's [user ID](https://techswift.org/2020/04/22/how-to-find-your-user-id-on-discord/).
        - `client.token` - Your discord bot's token.
        - `privateKey` - The private key of the account that will be sending funds. **Please be careful with the PK that you use, by my side, I've always done the tests with accounts that have funds only in testnets**
4. Start the bot.
    - Run `npm install` followed by `npm start` and let the faucet send funds to your community :).

## Support

```json
"networks": {
        "GOERLI": {
            "chainId": 5,
            "tokens": {
                "ETH": {
                    "amount": 0.001,
                    "isNativeToken": true
                }
            },
            "blockExplorer": "https://goerli.etherscan.io/tx/",
            "nodeUri": "<node-uri>"
        },
```

##### Adding new tokens

We have to add a new property in the `tokens` object with the name of our token, and add a `amount` and `address` field. For example, for adding the LINK token, we should do it this way:

```json
"networks": {
        "GOERLI": {
            "chainId": 5,
            "tokens": {
                "ETH": {
                    "amount": 0.001,
                    "isNativeToken": true
                },
            "blockExplorer": "https://goerli.etherscan.io/tx/",
            "nodeUri": "<node-uri>"
        },
```

After making this change, run `npm run update:faucet` to update the commands

##### Adding new networks

We have to add a new property in the `networks` object with the name of the network and add the fields: `chainId`, `blockExplorer` & `nodeUri`. For adding the mumbai network with the LINK token, we should do it this way:

```json
        "GOERLI": {
            "chainId": 5,
            "tokens": {
                "ETH": {
                    "amount": 0.001,
                    "isNativeToken": true
                },

            },
            "blockExplorer": "https://goerli.etherscan.io/tx/",
            "nodeUri": "<node-uri>"
        },
       
```

## Contributing

Contributions are always welcome!

Please adhere to this project's `code of conduct`.

