### [CMBTWallet](https://www.coinmarketbrasil.com.br/wallet/cmbt)


### `mercury` is the development branch. gh-pages contains only the smaller dist folder only and is served to Coinmarketbrasil.com.br/wallet/cmbt

- Our infrastructure ("node") is on AWS. [You can also use your own node.]


### CMBT Wallet

- CMBTWallet is a free, open-source, client-side tool for easily & securely interacting with the Ethereum network. As one of the leading providers of Ethereum services, MyEtherWallet equips users with an easy-to-understand and accessible suite of tools for their needs.
- It was created and is maintained by [kvhnuke](https://github.com/kvhnuke) and [tayvano](https://github.com/tayvano).

#### Features

- Create new wallets completely client side.
- Access your wallet via unencrypted private key, encrypted private key, keystore files, mnemonics, or Digital Bitbox, Ledger Nano S or TREZOR hardware wallet.
- Easily send ETH and *any* ERC-20 Standard Token. [Many tokens included as default.](https://myetherwallet.groovehq.com/knowledge_base/topics/can-i-send-my-steem-slash-btc-slash-ltc-slash-nem-slash-to-myetherwallet)
- Generate, sign & send transactions offline, ensuring your private keys never touch an internet-connected device.
- Securely access your ETH & Tokens on your [Digital Bitbox, Ledger or TREZOR Hardware Wallet](https://myetherwallet.groovehq.com/knowledge_base/topics/hardware-wallet-recommends) via the MyEtherWallet interface (Chrome & Opera natively, Firefox w/ [add-on](https://addons.mozilla.org/en-US/firefox/addon/u2f-support-add-on/))
- Now in 18 languages thanks 100% to the amazing Ethereum community.
- Supports URI Strings on Send Transaction Page.
    - to=[address]
    - value=[number]
    - sendMode=[ether | token]
    - tokenSymbol=[ARC | ICN | MKR | ....]
    - gasLimit=[number] OR gas=[number]
    - data=[hex data]
    



### Users (non-developers)

- [It is recommended you start here.](https://myetherwallet.github.io/knowledge-base/getting-started/getting-started-new.html)
- You can run MyEtherWallet.com on your computer. You can create a wallet completely offline & send transactions from the "Offline Transaction" page.

1. Go to https://github.com/kvhnuke/etherwallet/releases/latest.
2. Click on dist-vX.X.X.X.zip.
3. Move zip to an airgapped computer.
4. Unzip it and double-click index.html.
5. MyEtherWallet.com is now running entirely on your computer.

In case you are not familiar, you need to keep the entire folder in order to run the website, not just index.html. Don't touch or move anything around in the folder. If you are storing a backup of the MyEtherWallet repo for the future, we recommend just storing the ZIP so you can be sure the folder contents stay intact.

As we are constantly updating MyEtherWallet.com, we recommend you periodically update your saved version of the repo.




### Developers

If you want to help contribute, here's what you need to know to get it up and running and compiling.

- Both the Chrome Extension and the MyEtherWallet.com are compiling from the same codebase. This code is found in the `app` folder. Don't touch the `dist` or `chrome-extension` folders.
- We use angular and bootstrap. We used to use jQuery and Bootstrap until it was converted in April 2016. If you wonder why some things are set up funky, that's why.
- The mercury branch is currently the active development branch. We then push the dist folder live to gh-pages, which then gets served to MyEtherWallet.com.
- We use npm / gulp for compiling. There is a lot of stuff happening in the compilation.
- Old node setups can be found in in `json_relay_node` (node.js) & `json_relay_php` (php). These are great resources for developers looking to get started and launch a public node on a $40 Linode instance.

**Getting Started**

- Start by running `npm install`.
- Run `npm run dev`. Gulp will then watch & compile everything and then watch for changes to the HTML, JS, or CSS.
- For distribution, run `npm run dist`.

**Folder Structure**
- `fonts` and `images` get moved into their respective folders. This isn't watched via gulp so if you add an image or font, you need to run `gulp` again.
- `includes` are the pieces of the pages / the pages themselves. These are pretty self-explanatory and where you will make most frontend changes.
- `layouts` are the pages themselves. These basically take all the pieces of the pages and compile into one massive page. The navigation is also found here...sort of.
    * `index.html` is for MyEtherWallet.com.
    * `cx-wallet.html` is the main page for the Chrome Extension.
    * `embedded.html` is for https://www.myetherwallet.com/embedded.html.

- You can control what shows up on coinmarketbrasil.com.br vs the Chrome Extension by using: `@@if (site === 'cx' )  {  ...  }` and `@@if (site === 'mew' ) { ... }`. Check out `sendTransaction.tpl` to see it in action. The former will only compile for the Chrome Extension. The latter only to MyEtherWallet.com.
- `embedded.html` is for embedding the wallet generation into third-party sites. [Read more about it and how to listen for the address generated here.](https://www.reddit.com/r/ethereum/comments/4gn37o/embeddable_myetherwallet_super_simple_wallet/)
- The wallet decrypt directives are at `scripts/directives/walletDecryptDrtv.js`. These show up on a lot of pages.
- The navigation is in `scripts/services/globalServices.js`. Again, we control which navigation items show up in which version of the site in this single file.
- As of September 2016, almost all the copy in the .tpl files are only there as placeholders. It all gets replaced via angular-translate. If you want to change some copy you need to do so in `scripts/translations/en.js` folder. You should also make a note about what you changed and move it to the top of the file so that we can make sure it gets translated if necessary.
- `styles` is all the less. It's a couple custom folders and bootstrap. This badly needs to be redone. Ugh.

