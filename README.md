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

![Screenshot 2024-04-06 012012](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/9333164e-74d5-4908-a160-c719473c4570)

# Slither steps-

* Pull Docker Image for slither : docker pull trailofbits/eth-security-toolbox

* Run it : docker run -it --rm -v $PWD:/data trailofbits/eth-security-toolbox

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/75199822-99bc-4346-903b-2f347c3d9eaa)

* Now open another terminal

* Go to the root directory of the contract file (in my case data)

use cmd : sudo docker container ls to find container id

* This will basically provide you the container ID, image, and other relevant details of the container. We will require the container ID in the next command.
Now to copy sol file in the container:

sudo docker cp < path to solidity(flatten) file > “put-containner-id”:/<container file path>

Or

sudo docker cp $(pwd)/filename.sol “put-containner-id”:/home/ethsec

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/4776a796-6fcc-4c57-a1cd-3748024b3b0c)

* It has basically three components
* 
i. solidity contract file path

ii. container id (which we received from last command)

iii. container file path (go to the first terminal and write ‘pwd’ to get present directory of container)

So what this command basically does is it will copy the contract file and paste it inside the container environment so that we can run slither commands on it.

Go to the first terminal where the container environment is running. And, write the command:

slither filename.sol

* The second command we will run is:
  
slither-check-erc filename.sol <contract name in code>

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/1e2a9c0d-3d97-493a-b8a4-17d5804e96a7)

* So this command is for those smart contracts that are inheriting ERC features. And this command checks all the ‘must-have’ elements that an ERC token should have.






