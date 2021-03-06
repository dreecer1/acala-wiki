# Use Waffle

There are multiple tools you can use to develop and compile Solidity contracts, we'd present two here as options

* online web app Remix 
* Solidity development and testing framework Waffle

### Compile Solidity Contract using Waffle Comment

**Note:** you can skip this section if you compiled the smart contract with Remix.

This guide walks through the process of deploying a Solidity-based smart contract to Acala using [Waffle](https://github.com/EthWorks/Waffle). Waffle is one of the most commonly used smart contract development frameworks for Ethereum.

### **1. Check Prerequisites**

First, we need to install Node.js \(we use v15.x in this example\) and the npm package manager. You can do this by running in your terminal:

```text
curl -sL https://deb.nodesource.com/setup_15.x | sudo -E bash -
```

```text
sudo apt install -y nodejs
```

We can verify that everything installed correctly by querying the version for each package:

```text
node -v
```

```text
npm -v
```

### **2. Install Waffle**

We've made it easy by collecting all required dependencies in the [AcalaNetwork/evm-examples](https://github.com/AcalaNetwork/evm-examples) repo.

Simply clone the repository and install the dependencies.

```text
git clone https://github.com/AcalaNetwork/evm-examples
cd evm-examples

npm install 
# or
yarn install
```

Alternatively, you can install each library separately as the following: 

Create a folder

```text
mkdir smart-contract-waffle
cd smart-contract-waffle
```

Init npm dependencies

```text
npm init -y
```

Install all required dependencies

```text
npm i -D @openzeppelin/contracts@3.3.0 ethereum-waffle@3.2.1 
```

Note: it's recommended to install dependencies with exact versions as specified to avoid breaking changes.

Then create a waffle settings file

```text
touch waffle.json
```

Paste the following in the `waffle.json` file

```text
 {
    "compilerType": "solcjs",
    "compilerVersion": "0.6.2",
    "sourceDirectory": "./contracts",
    "outputDirectory": "./build"
  }
```

This sets up the solidity compiler with version `0.6.2`, compiles contracts from the `./contracts` folder, and saves the bytecode output and ABI files to `./build` folder.

### **3. Compile the Solidity Con**t**ract**

Now create the `./contracts` folder, and add the `BasicToken.sol` contract.

```text

mkdir contracts
touch contracts/BasicToken.sol
```

Paste the following content into the `BasicToken.sol` file and save.

```text
pragma solidity ^0.6.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

// Example class - a mock class using delivering from ERC20
contract BasicToken is ERC20 {
    constructor(uint256 initialBalance) public ERC20("Basic", "BSC") {
        _mint(msg.sender, initialBalance);
    }
}

```

Now compile the contract into ABI and bytecode. Run the following in the terminal

```text
npx waffle
```

### **4. Get the ABI file**

Waffle will then generate the output file `./build/BasicToken.json` into the `./build` folder. 

Note: this file should be the same as the one created with Remix.

Waffle also provides a full suite of testing utilities, check out their documentation and code samples [here](https://github.com/EthWorks/Waffle).

