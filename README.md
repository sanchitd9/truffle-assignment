# Truffle Tutorial

This repository contains code from the Truffle Tutorial here:
- [Part 1/4 - Installation, Contract Creation](https://youtu.be/ZaqAwOzEiQ8)
- [Part 2/4 - Migrations, Deployment](https://youtu.be/TDDuLlOiYJ8)
- [Part 3/4 - Testing](https://youtu.be/YKJkcg_ycpM)
- [Part 4/4 - Deployment](https://youtu.be/roHoOZXIxYs)

### **Part 1**
Part 1 of the tutorial involves installing the prerequisites needed to run and deploy a Truffle smart contract:
- NodeJS
- Truffle
- Ganache

### **Part 2**
Part 2 involves the creation of a simple smart contract called HelloWorld.
- This contract has a constructor which is used to initialize a string:
   ```
   constructor(string memory _message) {
       message = _message;
       owner = msg.sender;
   }
   ```
- The function *hello* returns the string initialized by the constructor:
  ```
  function hello() public view returns (string memory) {
      return message;
  }
  ```

  ![console_output](/output/Screenshot%202022-10-23%20173400.png)


- Finally, the function *setMessage* allows the user to change the value of the string:
  ```
  function setMessage(string memory _message) public payable {
      require(msg.value >= 1 ether);
      require(msg.sender == owner);
      message = _message;
  }
  ```

![console_output](output/Screenshot%202022-10-23%20173731.png)
![console_output](output/Screenshot%202022-10-23%20173840.png)

### **Part 3**
This part of the tutorial is focussed on writing unit tests for the smart contract.
- The first test checks if the *setMessage* function sets the value of the string correctly:
  ```
  it("constructor should set the message correctly", async () => {
      let instance = await HelloWorld.deployed();
      let message = await instance.message();
      assert.equal(message, "Hello World constructor");
  });
  ```
- The second test ensures that the owner's address is equal to the first value of the accounts array:
  ```
  it("owner should be accounts[0]", async () => {
      let instance = await HelloWorld.deployed();
      let owner = await instance.owner();
      assert.equal(owner, accounts[0]);
  });
  ```

### **Part 4**
Finally, part 4 deploys the smart contract on the goerli testnet network.
The transaction has been recorded [here](https://goerli.etherscan.io/tx/0xf2b5dd3b96d223365f4e7de4967321cd78bd723a4f64b6cf039e1246ee16b832).

![screenshot](output/Screenshot%202022-10-23%20174050.png)