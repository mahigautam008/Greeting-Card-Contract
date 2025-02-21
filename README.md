# 🎉 Greeting Card with ETH Gifting  

A simple Ethereum smart contract that allows users to send ETH along with a greeting message. The contract stores the latest greeting and the total ETH received.  

---

## 📌 Features  
✅ **Send ETH with a Greeting** – Users can send ETH along with a message.  
✅ **Stores the Last Greeting** – The contract saves the latest greeting message.  
✅ **View Contract Balance** – Anyone can check how much ETH is stored.  
✅ **Withdraw ETH** – The contract owner can withdraw ETH to any address.  
✅ **No Constructor Required** – No input is needed during deployment.  

---

## 📍 Deployed Contract  
- **Network:** Edu Chain  
- **Contract Address:** [`0xa0841e010ab087c31460dB87858436d5a678f92C`](https://explorer.educhain.io/address/0xa0841e010ab087c31460dB87858436d5a678f92C)  

---

## ⚡ How to Use  

### 1️⃣ Send a Greeting with ETH  
   - Call `sendGreeting("Your Message")` and send some ETH.  

### 2️⃣ Check Balance  
   - Call `getBalance()` to view the contract’s ETH balance.  

### 3️⃣ Withdraw ETH  
   - Call `withdrawETH(address)` to transfer ETH to a specific wallet.  

---

## 📜 Smart Contract Code (Solidity)
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract GreetingCard {
    string public lastGreeting;
    uint256 public totalReceived;

    event Greeted(address indexed sender, string message, uint256 amount);

    function sendGreeting(string memory _message) public payable {
        require(msg.value > 0, "Send some ETH to gift.");
        lastGreeting = _message;
        totalReceived += msg.value;

        emit Greeted(msg.sender, _message, msg.value);
    }

    function getBalance() public view returns (uint256) {
        return address(this).balance;
    }

    function withdrawETH(address payable _to) public {
        require(address(this).balance > 0, "No ETH to withdraw.");
        _to.transfer(address(this).balance);
    }
}
