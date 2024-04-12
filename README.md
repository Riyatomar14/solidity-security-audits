# solidity-security-audits

# 1.solgraph steps-

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

## Docker

```
# Pull the latest release of mythril/myth
$ docker pull mythril/myth
```

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

# 4. Surya steps-

for more info: https://github.com/Consensys/surya






