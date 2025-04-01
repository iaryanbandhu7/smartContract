# smartContract
# Arbitrum Public Key Verification Contract

This Solidity smart contract verifies that a given Ethereum address signed a specific message. It's designed to be deployed on the Arbitrum network.

## Contract Address (After Deployment)
0x208Ffd84441c9c10d10b2eD94089c7B43548E7D1
## Purpose

The `PublicKeyVerification` contract allows you to confirm that a message was signed by a specific Ethereum address. This is useful for:

* Authentication: Verifying user identities.
* Authorization: Controlling access to certain functions or resources.
* Proof of Ownership: Demonstrating ownership of a message or data.

## Features

* **Address Verification:** Compares the recovered address from a signature with a pre-defined address.
* **Message Hashing:** Uses the standard Ethereum message hashing format for compatibility.
* **Signature Recovery:** Recovers the signing address from a given message hash and signature.
* **Arbitrum Compatibility:** Designed for deployment on the Arbitrum network.

## Getting Started

### Prerequisites

* Node.js and npm (or yarn)
* Hardhat, Truffle, or Remix (for development and deployment)
* An Arbitrum node or provider (e.g., Infura, Alchemy)

### Deployment

1.  **Clone the Repository (if applicable):**
    ```bash
    git clone [your-repository-url]
    cd [your-project-directory]
    ```

2.  **Install Dependencies:**
    ```bash
    npm install # or yarn install
    ```

3.  **Configure Deployment:**
    * If using Hardhat or Truffle, configure your `hardhat.config.js` or `truffle-config.js` with your Arbitrum network settings and private key.
    * If using Remix, connect to the Arbitrum network.

4.  **Deploy the Contract:**
    * **Hardhat:** `npx hardhat run scripts/deploy.js --network arbitrum` (adjust the script and network name)
    * **Truffle:** `truffle migrate --network arbitrum`
    * **Remix:** Deploy directly from the Remix IDE.

5.  **Note the Contract Address:** The deployment process will output the contract address. Save this address, as you'll need it to interact with the contract.

### Usage

1.  **Prepare a Message and Signature:**
    * In a client-side application (e.g., using ethers.js), sign a message using the private key corresponding to the desired Ethereum address.
    * Obtain the message and the signature (65 bytes).

2.  **Interact with the Contract:**
    * Use a library like ethers.js or web3.js to connect to the deployed contract.
    * Call the `testVerify` or `verifyPublicKey` function, providing the message and signature.
    * The function will return `true` if the signature is valid and `false` otherwise.

    Example with ethers.js:

    ```javascript
    const ethers = require('ethers');
    const contractAddress = "[Insert Contract Address Here]";
    const contractABI = [/* Paste your contract ABI here */]; //Get this from the compilation.
    const provider = new ethers.providers.JsonRpcProvider("YOUR_ARBITRUM_RPC_URL"); //Replace with your RPC URL.
    const contract = new ethers.Contract(contractAddress, contractABI, provider);

    async function verifySignature(message, signature) {
        const result = await contract.testVerify(message, signature);
        console.log("Signature verification result:", result);
    }
    ```

### Contract Functions

* **`constructor(address _expectedAddress)`:** Initializes the contract with the expected Ethereum address.
* **`verifyPublicKey(bytes memory signature, bytes32 messageHash) public view returns (bool)`:** Verifies a signature against a message hash.
* **`recoverSigner(bytes32 messageHash, bytes memory signature) internal pure returns (address)`:** Recovers the signer's address from a signature.
* **`hashMessage(string memory message) public pure returns (bytes32)`:** Hashes a message using the Ethereum message prefix.
* **`testVerify(string memory message, bytes memory signature) public view returns(bool)`:** example function to verify, using hashMessage and verifyPublicKey.

### Security Considerations

* Hardcoded addresses should be managed carefully. Consider using a more flexible approach for production environments.
* Ensure that the signatures you verify are generated securely.
* Always validate user inputs to prevent unexpected behavior.

### Contributing

[Add information on how to contribute to your project.]

### License

[Add your license information.]
