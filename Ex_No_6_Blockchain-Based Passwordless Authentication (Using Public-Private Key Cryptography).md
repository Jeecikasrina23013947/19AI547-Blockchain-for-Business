# Experiment 6: Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography)
date:28.04.2025
# Aim:
To implement a secure passwordless authentication system using public-private key cryptography on Ethereum. This prevents phishing and password leaks.

# Algorithm:
Step 1:
Start the Ethereum environment (such as Ganache, or a Testnet) and deploy the smart contract that manages user registration and authentication.

Step 2:
User initiates registration by submitting their Ethereum public key to the smart contract.

Step 3:
The smart contract securely stores the public key associated with the user's account address.

Step 4:
During login, the server (or smart contract) generates a random challenge message (e.g., a random string or nonce).

Step 5:
The server sends the challenge to the user’s client-side application.

Step 6:
The user’s client-side application signs the challenge using their private key via cryptographic functions (e.g., web3.eth.personal.sign).

Step 7:
The signed challenge (digital signature) is sent back to the server (or smart contract) for verification.

Step 8:
The server (or smart contract) verifies the signature using the stored public key and checks whether the signature matches the original challenge.

Step 9:
If the verification is successful, the user is authenticated successfully; otherwise, access is denied.

Step 10:
End the process by granting access to authenticated users or sending an error message for failed authentication.

# Program:
NAME:JEECIKASRINA M
REG NO:212223100015
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PasswordlessAuth {
    mapping(address => bool) public registeredUsers;

    event UserRegistered(address user);
    event UserAuthenticated(address user);

    function registerUser() public {
        require(!registeredUsers[msg.sender], "Already registered");
        registeredUsers[msg.sender] = true;
        emit UserRegistered(msg.sender);
    }

    function authenticate(bytes32 hash, uint8 v, bytes32 r, bytes32 s) public view returns (bool) {
        require(registeredUsers[msg.sender], "User not registered");
        address signer = ecrecover(hash, v, r, s);
        return signer == msg.sender;
    }
}
```

# Expected Output:
![1](https://github.com/user-attachments/assets/620e1d54-b4f2-481f-aa8b-e6986e2fbc6a)
![2](https://github.com/user-attachments/assets/7d7153ec-214c-4a9a-9a34-a6119a04b6f0)
![3](https://github.com/user-attachments/assets/17fd63a6-a8a2-4067-9f7d-2772604b5353)
![5](https://github.com/user-attachments/assets/66612f2d-193b-4a68-9b6e-b5a8b63b1f22)
![6](https://github.com/user-attachments/assets/c0764497-e64b-4637-9eae-bf9a2125dfa7)

Users can register without a password.


Users sign a challenge with their private key for authentication.


The smart contract verifies signatures to confirm identity.



# High-Level Overview:
Eliminates password hacks & phishing attacks.


Uses Ethereum's built-in cryptographic functions.


Inspired by Web3 login solutions like MetaMask authentication.

# RESULT: 
THUS THE EXPERIMENT SUCCESSFULLY EXECUTED.
