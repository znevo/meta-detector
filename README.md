# meta-detector

A wrapper to simplify the process of interacting with metamask.

The goal is to provide quick access to common use cases for helping a user manage their connected wallet, and simple event handling for user interactions within metamask.

### Setup

Copy paste `MetaMask.js` and `MetaMaskEvent.js` into your project
(npm package coming soon!)

Install required dependencies

```
npm i @metamask/detect-provider
```

A tiny utility for detecting the MetaMask Ethereum provider, or any provider injected at `window.ethereum`
[https://github.com/MetaMask/detect-provider](https://github.com/MetaMask/detect-provider)

### Import

```
import Metamask from './MetaMask';
const metamask = new Metamask();
window.metamask = metamask;
```

### Initialize

Sets the provider, chain, and any previously connected accounts.

```
await metamask.init();
```


### Helpers

```
metamask.installed                     // (bool) is metamask installed
await metamask.connect();              // bind to 'connect wallet' button
await metamask.chain('rinkeby');       // bind to 'switch network' button
metamask.ready();                      // (bool) ready on mainnet
metamask.ready('rinkeby');             // (bool) ready on rinkeby
metamask.provider                      // the metamask provider
metamask.user                          // connected account address
```

### Event Handling

Subscribe a handler to an event

```
metamask.on('EVENT_ACCOUNT_CONNECTED', () => {
	window.location.reload()
});
```

Unsubscribe from an event

```
metamask.off('EVENT_ACCOUNT_CONNECTED');
```

Supported Events

```
EVENT_METAMASK_FOUND        // MetaMask is installed
ERROR_METAMASK_NOT_FOUND    // MetaMask is not installed
ERROR_MULTIPLE_WALLETS      // Multiple wallets were found
EVENT_CHAIN_CONNECTED       // The chain is connected
ERROR_CHAIN_UNAVAILABLE     // The chain could not be fetched
EVENT_ACCOUNT_REMEMBERED    // The account was remembered
ERROR_ACCOUNT_NOT_FOUND     // The account was not found
ERROR_ACCOUNT_UNAVAILABLE   // The account could not be fetched
ERROR_PERMISSION_REFUSED    // The connection attempt was refused
ERROR_PERMISSION_FAILED     // The connection attempt failed
EVENT_ACCOUNT_CONNECTED     // The account is connected
EVENT_ACCOUNT_DISCONNECTED  // The account was disconnected
EVENT_ACCOUNT_SWITCHED      // The account was switched
EVENT_CHAIN_SWITCHED        // The chain was switched
```