# Testing OZ Sapp

- clone this repo: `git clone git@github.com:fernandomg/oz-sapp.git`
- install project dependencies: `yarn install`
- initialize OpenZeppelin project: `npx oz init` (use default options)
- generate a new mnemonic: `npx mnemonics`
- go to infura and generate a new project key
- create `secrets.json` with the structure:

```json
{
  "mnemonic": "your mnemonics...",
  "projectId": "your infura project key"
}
```
- list accounts: `npx oz accounts` (pick `rinkeby` network)
- transfer funds to the `Default` account listed


- deploy contract: `npx oz deploy`
  - pick `upgradable`
  - pick `rinkeby` network
  - pick `Product` contract (the only one listed)
  - call a function to initialize? `Y` -> select `initialize` (the only listed) -> and set a value, i.e.: `1`
  - copy the address that is returned (this is the `Proxy` address (**A**), pointing to `Product` contract address, initialized to `1`)


- transfer ownership to your Safe: `npx oz set-admin <A> <your safe address>`
  - pick `rinkeby`
  - write down the last 4 chars of your safe, as stated in the Warning message.


- deploy again the same contract: `npx oz deploy`
  - **IMPORTANT** pick `regular` this time
  - pick `rinkeby` network
  - pick `Product` contract (the only one listed)
  - call a function to initialize? `Y` -> select `initialize` (the only listed) -> and set a value, i.e.: `2`
  - copy the address that is returned (this is the `Product` contract address (**B**), initialized to `2`)


- go to your safe, and load OpenZeppelin sApp: `https://ipfs.io/ipfs/QmQovvfYYMUXjZfNbysQDUEXR8nr55iJRwcYgJQGJR7KEA/`
  - on `Contract address`, paste the `Proxy` address (**A**)
  - on `New implementation address`, paste the `Product` contract address (**B**)
  - click `Upgrade` button
  - submit and follow with your typical Safe's flow


