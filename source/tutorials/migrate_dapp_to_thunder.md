# Migrate a DApp to Thunder

In this tutorial, we will be migrating an existing decentralized application (DApp) to Thunder.  We assume that your project has been set up using the popular tool [Truffle](http://truffleframework.com/), though the workflow should be easily adeptable to other tools.  If you are having trouble deploying an existing DApp to Thunder, drop a line at dev@thundertoken.com and we will be happy to help.

Since Thunder is 100% compatible with Ethereum, migrating an existing DApp to Thunder is as easy as installing a package and changing a couple lines in your config.

## Installing dependencies

Run the following command in your project's root directory (where the `contracts` directory is located):

```
npm install truffle-hdwallet-provider
```

## Update Truffle config

Open up `truffle.js` (or `truffle-config.js` if you are using Windows) and add the following code to the top of the file:

```javascript
let HDWalletProvider = require('truffle-hdwallet-provider')
let mnemonic = "<the mnemonic for your private key>"
```

Note that the `mnemonic` variable needs to be set to a real mnemonic.

Now, in your module exports, include a `thunder` section under the `networks` section, like the following:

```javascript
module.exports = {
  networks: {
    thunder: {
      provider: function() {
        return new HDWalletProvider(mnemonic, "https://testnet.thundertoken.com")
      },
      network_id: "*"
    }
  }
}
```

## Deploy smart contracts on Thunder

To deploy your smart contracts on Thunder, simply run:

```
truffle migrate --network thunder
```

If you didn't see any error messages, you should be all set.  It was that easy!

Note that smart contracts are only a part of the overall DApp.  For instance, you still need to customize your frontend so that it uses the smart contracts deployed on Thunder.  We won't detail the steps here since they are very much dependent on your specific project, but feel free to drop us a line at dev@thundertoken.com and we will be happy to help.
