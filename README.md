# Polygon Network Performance Benchmarking Test

## Overview

This project is designed to evaluate and benchmark the transaction processing capacity of the Polygon Network using free Infura. This project is designed to stress test the Polygon network by measuring its performance during intensive transaction and minting operations. The test consists of two main parts:

1. Sending multiple transactions within a minute.
2. Minting 1000 NFTs (Non-Fungible Tokens) and measuring the time it takes.


The project incorporates a wide array of features including transaction retry capability in case of failures, ability to fetch the latest gas price from the network, estimation of transaction costs before execution, usage of mnemonics and Hierarchical Deterministic Wallets (HD wallets) for seamless wallet configuration, easy and efficient funding methods for the wallets, adjustable concurrency and priority queue levels for transactions, and more.

## Tech Stack

This project is built using the following technologies:

- **Node.js:** A JavaScript runtime built on Chrome's V8 JavaScript engine.
- **TypeScript:** An open-source language which builds on JavaScript by adding static type definitions.
- **ethers.js:** A complete Ethereum wallet implementation and utilities in JavaScript and TypeScript.
- **dotenv:** A zero-dependency module that loads environment variables from a `.env` file.
- **es6-promise-pool:** A tiny, no-dependencies library that makes it easy to concurrently process many tasks with a limited concurrency level using Promises.
- **p-queue:** A promise queue with concurrency control.
- **crypto:** A built-in module in Node.js to handle cryptographic functions.
- **Redis:** An open-source, in-memory data structure store, used as a database, cache and message broker.

## Prerequisites

Make sure to have the following prerequisites before starting:

- Node.js (v14.x or newer)
- NPM (v7.x or newer) or Yarn (v1.22.x or newer)
- Redis server running locally or remotely
- An Infura account
- A private key for Polygon account
- A Polygon API key
- A Mnemonic phrase for HD Wallets

## Setup

1. **Clone the Repository**

   Use the following commands to clone the repository and navigate into the directory.

  With HTTPS:
   ```bash
   git clone https://github.com/integrations-Polygon/stress-test.git
   cd polygon-network-stress-test

   ```

   With SSH:
   ```bash
   git clone git@github.com:integrations-Polygon/stress-test.git
   cd polygon-network-stress-test
  ```

2. **Install Dependencies**

  Use npm or Yarn to install the dependencies.
  
  With npm:
  ```bash
  npm i
  ```

  With Yarn:

  ```bash
  yarn
  ```

3. **Configure Environment Variables**

  Copy the provided .example.env file and create a new .env file.
  ```bash
  cp .example.env .env
  ```
  Replace the placeholders in the .env file with your actual credentials:
  ```env
  PRIVATE_KEY=<your_private_key>
  INFURA_PROJECT_ID=<your_infura_project_id>
  EXPLORER_API_KEY=<your_ethercan_api_key>
  MNEMONICS=<your_mnemonic_phrase>
  ```

## Usage

Start the stress test by using the following commands:

With npm:
```bash
npm run stressTest
```

With Yarn:
```bash
yarn run stressTest
```

Upon starting, the program will prompt you to input the number of accounts to create and the number of tokens to mint per account.

## Features and Configurable Constants

This project offers a suite of robust features, designed to allow developers to customize the testing parameters and achieve a realistic and versatile environment for stress testing blockchain transactions. Each feature is fine-tuned to deliver precision and reliability for various scenarios and requirements.

- **Transaction Retry**: The system intelligently retries transactions in case of failure, eliminating the need for manual intervention and promoting seamless operation.
- **Latest Gas Price Retrieval**: This feature ensures the use of the most recent gas price, optimizing the balance between transaction speed and cost.
- **Transaction Estimation**: Prior to execution, each transaction is estimated, enabling predictable outcomes and avoiding unnecessary expenditure.
- **Multiple Wallets Setup**: Leveraging the power of HDNode and mnemonics, the system offers simplified setup and management of multiple wallets.

Each feature is complimented by a set of configurable constants, enhancing flexibility and control for the developer. These include:

```typescript
export const GAS_STATION_API_URL =
  'https://gasstation-testnet.polygon.technology/v2';

export const CONCURRENCY_LEVEL = 50;

export const PQUEUE_LEVEL = 1;

export const FUND = 1;
```

- **GAS_STATION_API_URL**: Refers to the API URL used to fetch the current gas prices. Developers can easily replace this with the URL of any preferred gas station API.
- **CONCURRENCY_LEVEL**: Controls the number of concurrent transactions, thereby managing the transaction rate. Considerations for this setting should include network congestion and server capacity.
- **PQUEUE_LEVEL**: This regulates the maximum number of promises concurrently processed by each wallet, effectively managing resource utilization and transaction load balance.
- **FUND**: A simple toggle that controls the wallet funding feature. Setting this to `1` enables automatic funding of wallets with zero balance, while `0` disables this function.

These constants are critical to fine-tuning the testing process, hence, developers should consider their system capabilities, network conditions, and testing goals when configuring these parameters. Please note that altering these constants may significantly impact the performance and results of your stress test.

## User Inputs

The testing process can be initiated with the `yarn run stressTest` or `npm run stressTest` command, which prompts two primary user inputs:`tokensPerAccount` and `numberOfAccounts`. These parameters play a crucial role in determining the performance and results of the stress test.

- **tokensPerAccount**: This parameter represents the number of NFT tokens minted by each wallet in each transaction. The suggested value for reaching the 1000 NFT mints per minute target is `20`.
- **numberOfAccounts**: This input defines the number of wallets to be set up for the test. The optimal value for achieving 1000 NFT mints in a minute under normal network conditions is `50`.

Together, these values (20 accounts minting 50 NFTs each) generate the desired 1000 NFT mints within a minute. However, these are suggested values and can be adjusted based on specific testing needs and network conditions. It's important to note that increasing these values may amplify the network load and might require proportionate hardware resources.

This project's flexibility allows you to set these parameters according to your testing requirements, ensuring you can simulate diverse scenarios based on your needs.

## Stress Test Outcome

During the stress test, we encountered a limitation with the free Infura service. The rate limit imposed by Infura caused most of the requests to be rejected or refused, resulting in reduced transaction throughput during the test. As a result, we were unable to achieve the desired 1000 transactions per minute using the free Infura service.

However, we were able to include 45 of our transactions (issueToken) into a single block: [38538077](https://mumbai.polygonscan.com/txs?block=38538077). It's worth noting that the criteria to have more of our transactions included in a single block depends on the network traffic. Lower network traffic increases the chances of including most of our transactions in a single block.

To achieve optimal transaction throughput during stress testing, we recommend utilizing a private RPC provider such as a paid Infura or other reputable service. Additionally, it's crucial to fine-tune the testing parameters, including concurrency level, queue level, gas price optimization, and wallet funding, based on the network conditions and desired test scenarios.

By employing these best practices and using a paid RPC provider, developers can obtain more accurate stress test results and better understand the true capabilities of the Polygon Network under real-world conditions.

Link to Demo video [stress-test-demo-video](https://drive.google.com/file/d/1xlER6z49Mocr4vtV0dcthCCdx3CuZ2Fo/view)

## Conclusion

The stress test provided valuable insights into the capabilities and limitations of the Polygon Network when subjected to high transaction and minting loads. While the free Infura service introduced rate limiting constraints, it is essential to understand that with a more robust and paid service, the performance can be significantly improved.

To achieve optimal results during stress testing, it is recommended to use private RPC providers and fine-tune the testing parameters accordingly. This will ensure more accurate stress test outcomes and a better understanding of the Polygon Network's performance under real-world conditions.

## Note

As a reminder, this stress test project is intended for testing purposes only and should not be used in production without proper modifications and security considerations. Always exercise caution when conducting stress tests on the live network and ensure you are complying with any usage guidelines and restrictions imposed by the network and RPC providers.


## License

This project is unlicensed

## Contact

Please reach out to the maintainer of this repository for further queries.

## Author

Gulam Rasul Shah
Github: @grsLammy

