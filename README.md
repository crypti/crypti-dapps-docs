[![Slack Status](http://slack.crypti.me/badge.svg)](http://slack.crypti.me)

# Crypti Dapps Documentation

Welcome to the Crypti Dapps documentation. Where you will find all the information needed to start developing decentralized applications on the Crypti blockchain.

## Contents

* [Setting up an Environment](EnvironmentSetup.md)
* [Creating a Basic Dapp](BasicDapp.md)
* [Creating a Messaging Dapp](MessagingDapp.md)
* [Adding a User Interface](UserInterface.md)
* [Introducing the DApp Toolkit](DappToolkit.md)
* [Creating a Custom Sidechain](Sidechain.md)

## Crypti Dapps


Crypti Dapps are decentralized application, that working in Sidechain, and allow developers create new decentralzied products, and use XCR or BTC in this projects.
It's means each dapp contains their own sidechain, blocks of this sidechain generated by dapps forgers, that will take fee for it.

Users of Dapps can easy deposit each Dapp, use deposited XCR in Dapp, and then withdrawal XCR from Dapp. Deposit/withdrawal it's special transactions in Crypti, that move your XCR funds from main Crypti chain,
to sidechain, and allow use this XCR in Dapp.

Just few examples of dapps and how it can work:

  * **Messaging Dapp** - Users deposits messaging Dapp, send message and pay fees for each message to owner of Dapp.
  * **Decentralized Exchange** - Users deposits decentralized exchange Dapp and pays fees for open new order, etc.
  * **Decentralized Torrent Traker** - Users posts new torrents files to Dapp and get XCR as "thanks" for sharing.

It's make for Crypti some economies and real world use, support Dapps developer.

## How to make Dapp?

All Dapps written in full-stack web technologies:

  * **Nodejs/Javascript** - for backend and frontend.
  * **CSS3/HTML5** - For UI.

A lot of developers already know all or some of this technlogoies, that allows developers fast and easy create new decentralized applications and take some profit.

Then using our Command Line Interface *crypti-cli* developer can easy generate new genesis block for sidechain, clone **Crypti Toolkit** as base project structure, easy create new contract.

Use our tutorials to know more how to make Dapps. All tutorials in this repository.

## Crypti Dapps working in Nodejs?

Yes, it's working in sandboxed Nodejs. We prevent 90% of low system calls with [Seccomp](https://en.wikipedia.org/wiki/Seccomp). It's because you can run master node only on Linux and can't run master node on Mac OS/Windows, but you can develop there.

So, when Crypti launch new Dapp, it's launch new Nodejs process, secured by Seccomp, and it communicate with Crypti via pipes. There is not limit of message size, we made some work to prevent it, because by default pipes have some limitations.

## Who is Dapp forgers?

It's forgers, who generate blocks in sidechain. This forgers approved by owner of Dapp, they will generate new blocks and get part of fees. It's done to make community interesting in support dapps by community nodes.

Genesis block contains base list of forgers, but it can be changed later. All operations with genesis block works via **crypti-cli**.

## How Deposit/Withdrawal works?

When you deposit or withdrawal, you send special type of transaction. In case of deposit, it's sent deposit transaction from mainchain, then Dapp recieve it, create new transaction, that will save transactionId in Dapp blockchain, to prevent double spending attack, and then it will add funds on your account.

All funds that was deposited stored on Dapp owner account. So, this funds don't real move from mainchain, it's just stored on owner account of Dapp. To prevent scam projects, and theft of Dapp funds, we added multisignature functional, and recommend to use open sourced Dapps, where one of known escrow under multisignature.

When you withdrawal you funds from Dapp, you send new transaction to withdrawal in Dapp, once this transaction applied in block, Dapp master nodes will create withdrawal transaction, that will send in mainchain, and mainchain will store transaction id from sidechain, to prevent double spending attacks.

# API

The API used to communicate between a Dapp and the Crypti blockchain can be found [here](http://docs.crypti.me).

# Further Help

The Crypti Foundation is ready and waiting to answer your questions.

So feel free to join our slack group at: [slack.crypti.me](slack.crypti.me).

Thank you for making Crypti your decentralized applications platform of choice.

**The Crypti Foundation**
