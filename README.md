# Hyperledger Fabric network for chaincode in dev mode

Pre Requisite - Hyperledger Binaries and HLF Pre-Requisites software are installed

# Following are the steps to run the setup
1. create a working folder, change directory to working folder
2. git clone https://github.com/ashwanihlf/sample_chaincodedevntest.git
3. sudo chmod -R 755 sample_chaincodedevntest/
4. cd sample_chaincodedevntest  

-- Need to open up 3 Terminal now

Terminal 1 (Current Terminal) - Start the network
1. docker-compose -f docker-compose-simple.yaml up

Terminal 2 (Open up a new one) - Build and start the chaincode
1. docker exec -it chaincode sh
2. go build -o samplecc
3. CORE_PEER_ADDRESS=peer:7052 CORE_CHAINCODE_ID_NAME=mycc:0 ./samplecc

Terminal 3 (Open another one)

1. docker exec -it cli bash
2.  peer chaincode install -p chaincodedev/chaincode/chaincode_example02/go -n mycc -v 0
3.  peer chaincode instantiate -n mycc -v 0 -c '{"Args":[""]}' -C myc
4. peer chaincode invoke -C myc -n mycc -c '{"function":"initCar","Args":["Ashwani","Blue","BMW"]}'
5. peer chaincode query -C myc -n mycc -c '{"function":"readCar","Args":["Ashwani"]}
