# LayerZero - omni chain contracts

// TODO: add MNEMONIC to .env file

Read [Whitepaper](https://layerzero.network/pdf/LayerZero_Whitepaper_Release.pdf)

LayerZero relies on two parties to transfer messages between on-chain endpoints:
* The Oracle &
* The Relayer

LayerZero enables devs to send secure messages across blockchains.

`Omnichain Interoperability Protocol`

LayerZero Endpoint has a non-reentrancy guard for both the send() and receive(), respectively. In other words, both send() and receive() can not call themselves on the same chain.

### Setup the project
```shell
npm install
```
 
 ### Run tests
```shell
npx hardhat test
```

### NOTE: You must add a .env with a MNEMONIC that is funded on testnets !
configure an .env file to have the values of .env.example and test deploy! (Use a real LayerZero endpoint in place of 0x0000..) 

# Testing Cross Chain Messages

1. Deploy both OmniCounters:

```
npx hardhat --network fuji deploy
npx hardhat --network mumbai deploy 
````

2. Set the remote addresses, so each contract can receive messages
```angular2html
npx hardhat --network mumbai omniCounterSetRemote --target-network fuji
npx hardhat --network fuji omniCounterSetRemote --target-network mumbai
```
3. Send a cross chain message from `mumbai` to `fuji` !
```angular2html
npx hardhat --network mumbai omniCounterIncrementCounter --target-network fuji
```

Optionally use this command in a separate terminal to watch the counter increment in real-time.
```
npx hardhat --network fuji omniCounterPoll    
```

# Testing Multiple Cross Chain Messages

1. Deploy both OmniCounters:

```
npx hardhat --network mumbai deploy 
npx hardhat --network fuji deploy
npx hardhat --network bsc-testnet deploy 
npx hardhat --network fantom-testnet deploy 
````

2. Set the remote addresses, so each contract can receive messages
```angular2html
npx hardhat --network mumbai omniCounterSetRemote --target-network fuji
npx hardhat --network fuji omniCounterSetRemote --target-network mumbai

npx hardhat --network mumbai omniCounterSetRemote --target-network bsc-testnet
npx hardhat --network bsc-testnet omniCounterSetRemote --target-network mumbai

npx hardhat --network mumbai omniCounterSetRemote --target-network fantom-testnet
npx hardhat --network fantom-testnet omniCounterSetRemote --target-network mumbai
```
3. Send a cross chain message from `mumbai` to `fuji` !
```angular2html
npx hardhat --network mumbai omniCounterIncrementMultiCounter --target-networks fuji,bsc-testnet,fantom-testnet
```

Optionally use this command in a separate terminal to watch the counter increment in real-time.
```
npx hardhat --network fuji omniCounterPoll
npx hardhat --network bsc-testnet omniCounterPoll
npx hardhat --network fantom-testnet omniCounterPoll
```

### For further reading, and a list of endpoint ids and deployed LayerZero contract addresses please take a look at the Gitbook here: https://layerzero.gitbook.io/


### Read the currently set Oracle
```npx hardhat --network mumbai omniCounterGetOracle --target-network fantom-testnet```

### Set a custom Oracle for the deployed OmniCounter
```npx hardhat --network mumbai omniCounterSetOracle --target-network mumbai --oracle 0xORACLE_ADDR```



### See some examples in `/contracts`  🙌

test LayerZero locally using LayerZeroEndpointMock.sol