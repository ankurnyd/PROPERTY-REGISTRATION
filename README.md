# PROPERTY-REGISTRATION
PROPERTY REGISTRATION _ Hyperledger
Introduction.
There are two smart contracts, 1) for User and 2) Registrar. NodeJS is used to write these smart contracts.
Pre-requisites
These smart contracts were developed using the VM provided by Upgrad which contains necessary software for deploying and executing smart contracts.
Users
• Seller – ankurnyd1, ankurnyd1@gmail.com, 1234123412341231
• Buyer – ankurnyd2, ankurnyd2@gmail.com, 1234123412341232
Step 1: Bootstrap the network
a) Command
• Go to the ‘network’ folder of the project • Execute the command ./fabricNetwork.sh up, which will prompt for the confirmation to boot the network. Enter ‘Y’ in the terminal to bring up the network.
2
June 7, 2021 2
Step 2: Chaincode Installation and Instantiation
b) Command:
• Once Step1 is complete, execute below command which will install & instantiate the smart contracts in Chaincode container and allow us to invoke different methods listed below. • ./fabricNetwork.sh install
3
June 7, 2021 3
Step 3: Start the Chaincode node application.
This is a must have step before proceeding to Step 4
Command: • Enter into docker container for chaincode using command docker exec -it chaincode /bin/bash • Install node modules using ‘npm install’ command which will install all necessary Node modules inside chaincode container. • Start the node application: npm run start-dev
4
June 7, 2021 4
Step 4: Invoke Smart Contract Methods
Method 1: requestNewUser
Commands:
• Enter into CLI container by having docker exec -it cli /bin/bash • Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:requestNewUser","ankurnyd1","ankurnyd1@gmail.com","1234567890","1234123412341231"]}'
5
June 7, 2021 5
Method 2: approveNewUser
Commands:
• Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.registrar:approveNewUser","ankurnyd1","1234123412341231"]}'
Method 3: recharge Account
Commands:
1. Enter into CLI container by having docker exec -it cli /bin/bash
2. Execute command: a. Success: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:rechargeAccount","ankurnyd1","1234123412341231","upg500"]}'
b. Failure: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:rechargeAccount","ankurnyd1","1234123412341231","upgr500"]}'
Success:
Failure:
6
June 7, 2021 6
Method 4: viewUser
Commands for Users Org:
• Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:viewUser","ankurnyd1","1234123412341231"]}'
Commands for Registrar Org:
• Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.registrar:viewUser","ankurnyd1","1234123412341231"]}'
Method 5: propertyRegistrationRequest
Commands: • Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:propertyRegistrationRequest","001","200","ankurnyd1","1234123412341231"]}'
7
June 7, 2021 7
Method 6: approvePropertyRegistration
Commands: • Enter into Peer0 of registrar org: Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.registrar:approvePropertyRegistration","001"]}'
Method 7: viewProperty
Commands for Users Org: • Enter into Peer0 of registrar org: Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:viewProperty","001"]}'
Commands for Registrar Org: • Enter into Peer0 of registrar org: Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.registrar:viewProperty","001"]}'
8
June 7, 2021 8
Method 8: updateProperty
Commands: • Enter into Peer0 of registrar org: Enter into CLI container by having docker exec -it cli /bin/bash
• Execute command: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:updateProperty","001","ankurnyd1","1234123412341231","onSale"]}'
Method 9: purchaseProperty
Pre-requisite:
In order to purchase property, we need to register new user as mentioned below before proceeding with purchase of the property.
Steps to register new user (ankurnyd2) in the network and request property purchase
• requestNewUser: peer chaincode invoke -o orderer.property-registration-network.com:7050 -C registrationchannel -n regnet -c'{"Args":["org.property-registration-network.regnet.users:requestNewUser","ankurnyd2","ankurnyd2@gmail.com","1234567892","1234123412341232"]}'
