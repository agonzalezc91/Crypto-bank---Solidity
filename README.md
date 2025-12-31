CryptoBank Smart Contract (Solidity)

A simple multi-user crypto bank smart contract written in Solidity.
This project allows users to deposit and withdraw ETH, while enforcing balance limits and basic access control.

The contract is designed as an educational project to practice Solidity fundamentals such as mappings, payable functions, events, access control, and safe ETH transfers.

Features

Multi-user ETH deposits

Users can only withdraw their own deposited ETH

Maximum balance per user enforced

Admin-controlled maximum balance

Safe ETH withdrawals using the Checks-Effects-Interactions (CEI) pattern

Event emission for deposits and withdrawals

Roles
Users

Can deposit ETH up to the maximum allowed balance

Can withdraw only the ETH they previously deposited

Admin

Can modify the maximum balance per user

The admin address is set at deployment time.

Contract Logic

Each user has an individual balance stored using:

mapping(address => uint256) public userBalance;

Rules enforced by the contract:

A user cannot deposit more ETH than maxBalance

A user cannot withdraw more ETH than their own balance

Security Considerations

Withdrawals follow the Checks-Effects-Interactions (CEI) pattern:

Checks (require)

Effects (state update)

Interactions (ETH transfer)

ETH transfers are executed using low-level .call

Transactions revert if the ETH transfer fails

Users cannot affect balances other than their own

Contract Functions
depositEther() (payable)

Allows a user to deposit ETH into the bank, provided their balance does not exceed maxBalance.

withdrawEther(uint256 amount)

Allows a user to withdraw ETH previously deposited.

modifyMaxBalance(uint256 newMaxBalance)

Allows the admin to update the maximum balance limit.

Events

EtherDeposit(address user, uint256 amount)

EtherWithdraw(address user, uint256 amount)

Events can be used to track deposits and withdrawals off-chain.

How to Test in Remix

Open https://remix.ethereum.org

Create a file called CryptoBank.sol

Paste the contract code

Compile using Solidity version 0.8.24

Deploy the contract with:

maxBalance_: maximum allowed balance per user (in wei)

admin_: admin address

Use different accounts to:

Deposit ETH with depositEther()

Withdraw ETH with withdrawEther()

Modify the maximum balance using the admin account

Notes

This contract is intended for learning and demonstration purposes

It does not include interest, fees, or dispute resolution

Direct ETH transfers to the contract (without calling depositEther) are not supported

Possible Improvements

Add receive() to support direct ETH transfers

Add pause/unpause functionality

Add withdrawal limits or fees

Add unit tests using Foundry or Hardhat

Refactor using custom errors instead of require strings

Author

Personal learning project developed as part of a journey into Solidity and Web3 development.
