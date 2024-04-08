# solidity-security-audits

## pre-requisites

* Install https://github.com/Riyatomar14/Docker

* Pull https://www.npmjs.com/package/solgraph : docker pull devopstestlab/solgraph
  


# create the smart contract in solidity:

$ sudo mkdir data

$ cd data

$ sudo vi MyContracts.sol

Run this smart contract in the docker image we just pulled : docker run -it --rm -v $PWD:/data devopstestlab/solgraph

you can see image by : xdg-open MyContracts.sol.png

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/fe368de5-479c-4405-910e-d9f399d72cba)

# Slither steps-

* Pull Docker Image for slither : docker pull trailofbits/eth-security-toolbox

* Run it : docker run -it --rm -v $PWD:/data trailofbits/eth-security-toolbox


