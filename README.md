# solidity-security-audits

# 1. solgraph steps-

## pre-requisites

for more info : https://www.npmjs.com/package/solgraph 

* Install https://github.com/Riyatomar14/Docker

```
docker pull devopstestlab/solgraph
```

# create the smart contract in solidity:

```
sudo mkdir data
```
```
cd data
```
```
sudo vi MyContracts.sol
```

```
contract MyContract {
    uint balance;

    function MyContract() {
      Mint(1000000);
   }

   function Mint(uint amount)
 internal {
     balance = amount;
}

  function Withdraw() {
     msg.sender.send(balance);
}


  function GetBalance() constant 
returns(uint) {
  return balance;
 }
}
```

Run this smart contract in the docker image we just pulled : 

```
docker run -it --rm -v $PWD:/data devopstestlab/solgraph
```

you can see image by :

```
xdg-open MyContracts.sol.png
```

![Screenshot 2024-04-06 012012](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/9333164e-74d5-4908-a160-c719473c4570)

# 2. Slither steps-

for more info:https://medium.com/@abhijeet.sinha383/test-solidity-contract-file-using-slither-testing-tool-4f7e3e8692dd

* Pull Docker Image for slither :
  
  ```
  docker pull trailofbits/eth-security-toolbox
  ``` 

* Run it :
  
```
docker run -it --rm -v $PWD:/data trailofbits/eth-security-toolbox
```

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/75199822-99bc-4346-903b-2f347c3d9eaa)

* Now open another terminal

* Go to the root directory of the contract file (in my case data)

use cmd :to find container id

```
sudo docker container ls
```

* This will basically provide you the container ID, image, and other relevant details of the container. We will require the container ID in the next command.
Now to copy sol file in the container:

```
sudo docker cp < path to solidity(flatten) file > “put-containner-id”:/<container file path>
```

Or

```
sudo docker cp $(pwd)/filename.sol “put-containner-id”:/home/ethsec
```

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/4776a796-6fcc-4c57-a1cd-3748024b3b0c)

* It has basically three components

i. solidity contract file path

ii. container id (which we received from last command)

iii. container file path (go to the first terminal and write ‘pwd’ to get present directory of container)

So what this command basically does is it will copy the contract file and paste it inside the container environment so that we can run slither commands on it.

Go to the first terminal where the container environment is running. And, write the command:

```
slither filename.sol
```

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/ec16745a-b262-474c-bd31-e5e7159c2875)

* The second command we will run is:
  
```
slither-check-erc filename.sol <contract name in code>
```

![image](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/9d6fbe3c-d73f-4b15-8359-354117cccf10)

* So this command is for those smart contracts that are inheriting ERC features. And this command checks all the ‘must-have’ elements that an ERC token should have.

# 3. Mythril steps-

for more info : https://mythril-classic.readthedocs.io/en/master/installation.html

## PyPI on Ubuntu

```
# Update
sudo apt update

# Install solc
sudo apt install software-properties-common
sudo add-apt-repository ppa:ethereum/ethereum
sudo apt install solc

# Install libssl-dev, python3-dev, and python3-pip
sudo apt install libssl-dev python3-dev python3-pip

# Install mythril
pip3 install mythril
myth version
```
![Screenshot 2024-04-12 200610](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/bd38cbe5-b479-43fe-9a9d-6257cd356d18)

## Docker

```
# Pull the latest release of mythril/myth
$ docker pull mythril/myth
```
![Screenshot 2024-04-12 200654](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/4af79c5d-5a23-4d6f-841c-24771f5d16e4)

## Use docker run mythril/myth the same way you would use the myth command

```
docker run mythril/myth --help
docker run mythril/myth disassemble -c "0x6060"
```
## To pass a file from your host machine to the dockerized Mythril, you must mount its containing folder to the container properly. For contract.sol in the current working directory, do:

```
contract Exceptions {

    uint256[8] myarray;
    uint counter = 0;
    function assert1() public pure {
        uint256 i = 1;
        assert(i == 0);
    }
    function counter_increase() public {
        counter+=1;
    }
    function assert5(uint input_x) public view{
        require(counter>2);
        assert(input_x > 10);
    }
    function assert2() public pure {
        uint256 i = 1;
        assert(i > 0);
    }

    function assert3(uint256 input) public pure {
        assert(input != 23);
    }

    function require_is_fine(uint256 input) public pure {
        require(input != 23);
    }

    function this_is_fine(uint256 input) public pure {
        if (input > 0) {
            uint256 i = 1/input;
        }
    }

    function this_is_find_2(uint256 index) public view {
        if (index < 8) {
            uint256 i = myarray[index];
        }
    }

}
```

## To pass a file from your host machine to the dockerized Mythril, you must mount its containing folder to the container properly. For contract.sol in the current working directory, do:

```
docker run -v $(pwd):/tmp mythril/myth analyze /tmp/Riya.sol
```
*(in my case my directory--> Riya)

![Screenshot 2024-04-12 200721](https://github.com/Riyatomar14/solidity-security-audits/assets/143107173/3d54d312-bf1b-469d-a9de-84062d46adbb)

# 4. Surya steps-

for more info: https://github.com/Consensys/surya

## Surya install

Pre-requisites:
```
NodeJS
NPM
```
Install Surya using npm:
```
npm install -g surya
```
Navigate to the directory where your solidity contracts are written & execute the following commands:

  - Parse your smart contract (create a tree like structure)
    ```
    surya parse mycontract.sol
    ```
    ![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/a531c013-3302-4eef-a2a1-4332e78d978c)

  - Flatten:
    ```
    surya flatten mycontract.sol
    ```
  - Describe (give a concise summary)
    ```
    surya describe mycontract.sol
    ```
    ![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/e05d45e1-187d-482c-8c7f-3f34e5e79e89)
    
# 4. Manticore steps- 

## pull the docker image for manticore

         sudo docker pull trailofbits/manticore
    
![image](https://github.com/RupeshKumar4511/Blockchain-Technology/assets/149661006/0175889b-ab4b-421b-9694-90cdf20570c8)

## make a directory
   
      mkdir audits2
   
## change the directory
   
      cd audits2
   
## run the command
   
      vim -vi
   
## And then write the smart contract and save the contract file with .sol extension.(for example Storage.sol)
   
![image](https://github.com/RupeshKumar4511/Blockchain-Technology/assets/149661006/fa046006-a95b-4cc9-ad4c-ffdf3bb0f7ec)


## Then run command
   
    manticore Storage.sol 







