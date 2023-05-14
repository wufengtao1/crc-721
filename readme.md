# CRC-721 Deployment Tutorial

> Before reading this tutorial, please read the following two points to familiarize yourself with the content and environment:

> 1. [Conflux Tree Diagram Blockchain "Digital Collection" Contract Standards and Writing Specifications]((https://conflux-technical-support.gitbook.io/conflux-nft-kai-fa-zhi-nan/)
> 2. [Conflux IDE environment configuration](https://chainide.gitbook.io/chainide-english-1/ethereum-ide-1/4.-conflux-ide/conflux-environment-configuration)

## Introduction
ChainIDE is a cloud-based smart contract IDE on which developers can write smart contracts for deployment on different blockchains such as Ethereum, BNB Chain, Polygon, Conflux, Nervos, Dfinity, Flow, Chain33, FISCO BCOS, etc.
It reduces the development cycle and save the user's time and energy.
If you have any questions, please join our [ChainIDE Discord](https://discord.gg/QpGq4hjWrh) and ask us questions.

## Prerequisite
1. ChainIDE
2. Fluent Wallet
3. Solidity
4. IPFS 

## What you need to do:
Follow the steps below to deploy your CRC-721 smart contract on the Conflux core testnet:

1. Install Fluent Wallet
2. Write a CRC-721 smart contract
3. Compile a CRC-721 smart contract
4. Deploy a CRC-721 smart contract
5. Create a flatten contract for verification
7. Verify the deployed contract on ConfluxScan
7. Contract application payment
7. Digital collection MINT

### Install Fluent Wallet
Fluent Wallet is a good choice when we want to interact with smart contracts on the Conflux blockchain.

Use Chrome, Firefox, or Edge browser to open Fluent official website [fluentwallet](https://fluentwallet.com/) and add the browser extension.

![image-20220623171235514](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220623171235514.png)

### 2. Write a CRC-721 smart contract
You need to write down all the necessary functions implemented in the ERC-721 smart contract. A general ERC-721 smart contract needs to contain the following functions:

 - balanceOf(): Returns the number of NFTs owned by the user
 - ownerOf(): returns the address of the token holder
 - approve(): Grant the address *to* the control of tokenId, and the Approval event needs to be triggered after the method succeeds.
 - setApprovalForAll(): grant the address_operator the control over all NFTs, and trigger the ApprovalForAll event after success.
 - getApproved(), isApprovedForAll(): Used to query authorization.
 - safeTransferFrom(): Transfer NFT ownership, a successful transfer operation must initiate a Transer event.
 - transferFrom(): Used to transfer NFTs, the Transfer event needs to be triggered after the method succeeds. The caller confirms that the _to address can receive the NFT normally, otherwise the NFT will be lost. When this function is implemented, it needs to check whether the judgment condition is met.

In Conflux, all CRC-721 contracts must also **must include** all enumeration functions in the following contracts:

* ERC721Enumerable: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/extensions/ERC721Enumerable.sol
* CRC721Enumerable: https://github.com/conflux-fans/conflux-contracts/blob/main/contracts/token/CRC721/extensions/CRC721Enumerable.sol

ChainIDE team has prepared a CRC-721 contract including all required functions, you can use this built-in template and add/remove some functions according to your requirements.

Open [ChainIDE official website](https://chainide.cn/zh-CN/) and click "Quick Start".

![image-20220624135448935](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220624135448935.png)

Click "New Project" and select CRC721 Showcase in Conflux

![image-20220624135743522](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220624135743522.png)

Now you can see the contract CRC721NatureAutoIdFixedMetadata.sol we prepared, which contains all the necessary functions, click it, it can set a separate Metadata URL for each NFT of MINT.

![image-20220627103648450](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627103648450.png)

### 3. Compile a CRC-721 smart contract
After completing your smart contract, it's time to compile the smart contract.
To compile, please go to the compile module, select an appropriate compiler based on your source code, and press the compile button. After successful compilation, the ABI and bytecode of the source code will be generated.
If there are some errors in your source code, they will be displayed under the console panel.
You may need to read the error carefully, resolve it accordingly and compile again!

**Please make a note of your source code's compiler version and license with optimization enabled** as you will need it when you verify your smart contract on confluxscan.

![image-20220624135104985](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220624135104985.png)

### 4. Deploy a CRC-721 smart contract
After the compilation is successful, it's time to deploy your compiled CRC-721 smart contract to the Conflux core testnet.
To do this, you need to install a Fluent Wallet first, add Conflux core testnet to your Fluent Wallet, and you need to receive some test coins to pay for gas, for this, you can do this.

* Click "Not Connected" in the upper right corner - "Injected Web3 Provider" - "Fluent Wallet"

![image-20220627104401269](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627104401269.png)

![image-20220627111457678](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627111457678.png)

* After connecting, make sure the network in the lower right corner is "Conflux Test Network", if not, click "Switch Network" to switch to "Test Network"; click "Deposit CFX" to get test coins.

![image-20220627111959393](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627111959393.png)

Then enter the "Depoly & Interaction" module, select the contract you want to deploy in the compiled smart contract and deploy it.

In this tutorial, we will use the CRC721NatureAutoIdFixedMetadata smart contract for deployment.

In the constructor parameters, name_ is the full name of the digital collection you want, symbol_ is the token name of the digital collection you want, and click "Deploy" after confirmation.

![image-20220627112547226](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627112547226.png)

After the deployment is successful, you can see a message in the console section, indicating that your smart contract has been successfully deployed.

### 5. Create a flattened contract for verification

To verify a smart contract that imports other smart contracts,
We need to create a flat file,
A flat file puts the source code of all imported contracts in one file,
To create a flattener file, you need to first add a "flattener" plugin.


![image-20220627112839722](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627112839722.png)

Once the Flatterner plugin is activated, you can access it by clicking on the right side of the screen, as shown in the image below.
Select the compiled file and click the Flatten button to create a flattened file, once the flattened file is created.
 It will be automatically copied to the clipboard.
You can paste it into a file and save it for later.

![image-20220627113039254](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627113039254.png)


If you want to save the flattened file, click the save button, and a flattened contract will be saved in the current warehouse.


![image-20220627113059356](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627113059356.png)

Saved flat contracts can be accessed under the explorer module.


![image-20220627113128014](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627113128014.png)

### 6. Verify the deployed contract on ConfluxScan

To verify a previously deployed smart contract, click here.


![image-20220627113450559](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627113450559.png)

Click "Contract" - "Verify Your Contract" below.

![image-20220627113542857](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627113542857.png)

Once you click on "Verify your Contract", you will be asked to provide the following.

 - Contract address: the address of the deployed smart contract you want to verify (filled in by default)
 - Contract name: the file name of the smart contract
 - License agreement: The license agreement at the beginning of the smart contract
 - Compiler: The compiler version selected for the original compilation
 - Optimization: Whether to enable optimization when compiling (if it is selected at that time, then run and select 200)
 - Contract source code: contract code after flatten

After confirmation, click "Submit"

![image-20220627114132354](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627114132354.png)


Your smart contract has been verified, congratulations!

 ![image-20220627114319231](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627114319231.png)

### 8. Contract application payment

Conflux’s payment mechanism subsidizes the user’s use of smart contracts through a sponsorship mechanism. By introducing a built-in payment contract, interacting with sponsored contracts will not need to spend CFX to pay gas fees, allowing new accounts with a balance of zero It is also possible to invoke smart contracts.

Therefore, please be sure to **introduce the proxy payment contract** in your contract, and set **Gas Fee Payment** to ensure that any user interacting with your contract can be sponsored by the proxy payment mechanism without spending CFX. In the current environment, this is very important for the compliance of your NFT application. ChainIDE CRC721 Showcase is configured with proxy payment by default.

> If the project party wants to get help in setting up payment, please contact Cike: cike@confluxnetwork.org
>
> For details of the payment mechanism, please refer to: https://forum.conflux.fun/t/conflux/11949

![image-20220627114718514](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627114718514.png)

Enter your contract address and press the Enter key, and click Apply after confirming that it is correct.

![image-20220627115137645](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627115137645.png)

### 7. Digital Collections Mint

To mint a digital stash you need to use the **mint function** with the wallet address of the person you want to airdrop the digital stash to,
 The _metadata input column is the corresponding metadata address,
 Before Mint, you need to generate Metadata, and the decentralized storage of metadata can better ensure that the NFT cannot be tampered with. To this end, Chainide provides two ways to generate metadata.

#### 1. Use the built-in html of chainide to upload the metadata to IPFS.


![image-20220627115434717](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627115434717.png)


![image-20220627115853038](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627115853038.png)

When the above method encounters 504, the second method can be used

#### 2. Use [pinata](https://www.pinata.cloud/), which is a website dedicated to uploading files to IPFS (other uploading IPFS websites are also available, such as [nft storage](https ://nft.storage/).

First, prepare the pictures to be uploaded. Here, rock, scissors, and cloth are taken as examples. The corresponding IDs are 1, 2, and 3, and they are placed in the same folder.

![image-20220701170302373](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701170302373.png)

Then enter [pinata](https://www.pinata.cloud/), a webpage dedicated to uploading files to IPFS.

Click "Upload" - "Folder" - select the folder containing the rock-paper-scissors images and upload them to IPFS.

![image-20220701172546437](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701172546437.png)

![image-20220701172620417](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701172620417.png)

After the upload is successful, enter the folder, click the name of the picture, and you can see the picture stored on IPFS.

![image-20220701175341505](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701175341505.png)

We will use the information after ipfs/ in the address bar later, pay attention to it.

![image-20220701175913228](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701175913228.png)

Next, we need to create a corresponding number of json files and upload them to IPFS (3 here)

Here is the URI rule for ERC1155 (compatible with ERC721)

* The json file name must be a hexadecimal lowercase alphanumeric without a 0x prefix.
* must be filled with 0 to a length of 64 hexadecimal characters

Metadata template:
```json
{
    "title": "Token Metadata",
    "type": "object",
    "properties": {
        "name": {
            "type": "string",
            "description": "Identifies the asset to which this token represents"
        },
        "decimals": {
            "type": "integer",
            "description": "The number of decimal places that the token amount should display - e.g. 18, means to divide the token amount by 1000000000000000000 to get its user representation."
        },
        "description": {
            "type": "string",
            "description": "Describes the asset to which this token represents"
        },
        "image": {
            "type": "string",
            "description": "A URI pointing to a resource with mime type image/* representing the asset to which this token represents. Consider making any images at a width between 320 and 1080 pixels and aspect ratio between 1.91:1 and 4:5 inclusive."
        },
        "properties": {
            "type": "object",
            "description": "Arbitrary properties. Values may be strings, numbers, object or arrays."
        }
    }
}
```
Therefore, create a new folder locally and create 3 new json files. The folder name and content are as follows, **and replace the link behind the image with ipfs:// plus the above IPFS image suffix** (eg: ipfs:/ /QmTj1D7wFN9wjW7toQhaKmkRpq6W4L3V5Q1VE274bLETn8/1.jpg):

000000000000000000000000000000000000000000000000000000000000000001.json

```json
{
    "name": "Rock",
    "description": "Rock Paper Scissors",
    "image": "ipfs://QmTj1D7wFN9wjW7toQhaKmkRpq6W4L3V5Q1VE274bLETn8/1.jpg",
    "properties": {
        "like": "scissors",
        "hate": "papper",
        "rarity": "common"
    }
}
```
![image-20220701180402498](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701180402498.png)

00000000000000000000000000000000000000000000000000000000000000002.json

```json
{
    "name": "Paper",
    "description": "Rock Paper Scissors",
    "image": "ipfs://QmTj1D7wFN9wjW7toQhaKmkRpq6W4L3V5Q1VE274bLETn8/2.jpg",
    "properties": {
        "like": "Rock",
        "hate": "Scissors",
        "rarity": "common"
    }
}
```
![image-20220701180558765](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701180558765.png)

0000000000000000000000000000000000000000000000000000000000000003.json

```json
{
    "name": "Scissors",
    "description": "Rock Paper Scissors",
    "image": "ipfs://QmTj1D7wFN9wjW7toQhaKmkRpq6W4L3V5Q1VE274bLETn8/3.jpg",
    "properties": {
        "like": "Paper",
        "hate": "Rock",
        "rarity": "common"
    }
}
```


![image-20220701180626097](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701180626097.png)

![image-20220701180840933](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701180840933.png)

Upload this folder containing 3 json files to IPFS via Pinata

![image-20220701180940682](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701180940682.png)

The red box in the figure is the CID of gamejson'

![image-20220701181117511](https://d3gvnlbntpm4ho.cloudfront.net/ERC1155+deployment+on+Rinkeby+Etherum/image-20220701181117511.png)

Enter the gamejson folder

![image-20220715094434847](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220715094434847.png)

Click on a json file (eg: 0000000000000000000000000000000000000000000000000000000000000001.json)

Copy the field after the link https://gateway.pinata.cloud/ipfs/ (for example: QmY4qTkh8jWL6zmGnDrNGZVWTTmiHhJaw3CnheJrJNKWcU/0000000000000000000000000000000000000000000000000000000000000000)

![image-20220715094646057](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220715094646057.png)

Add ipfs:// in front of the field to be the metadata link（add：ipfs://QmY4qTkh8jWL6zmGnDrNGZVWTTmiHhJaw3CnheJrJNKWcU/0000000000000000000000000000000000000000000000000000000000000001.json）

#### 3. After the metadata is uploaded, return to chainide for mint

to is the address you want to airdrop, and metadata is the metadata link (for example, the metadata link of method 1 is ipfs.io/ipfs/xxxxxxxxxxxxxx, and the method 2 is ipfs://xxxxxxxxxxxx)

![image-20220627141256220](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627141256220.png)

After Mint is successful, you can view your digital collection on Conflux Scan!

![image-20220627141402351](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627141402351.png)


![image-20220627142504721](https://d3gvnlbntpm4ho.cloudfront.net/CRC+721+Deployment+on++Conflux/image-20220627142504721.png)

Congratulations, you released your own digital collection on Conflux, very cool!









