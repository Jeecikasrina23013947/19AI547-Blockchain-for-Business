### Experiment 1: Decentralized Certificate Verification
DATE:16.04.2025
## Aim:
  To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity.
## Algorithm:
### Step 1:
Deploy a smart contract on a blockchain platform (e.g., Ethereum) to issue and verify certificates.

### Step 2:
Define a structure to store certificate details (ID, student name, course, issue date, certificate hash).

### Step 3:
Universities issue certificates by submitting certificate details and storing the hash of the certificate data in the smart contract.

### Step 4:
Use a cryptographic hashing function (e.g., keccak256) to generate a unique hash of the certificate data.

### Step 5:
Store the certificate hash and details (ID, student name, course, etc.) on-chain in the smart contract.

### Step 6:
Implement a function to verify the certificate by comparing the stored hash with the hash of the provided certificate data.

### Step 7:
Users input the certificate ID and certificate data they want to verify. The smart contract compares the input data's hash with the stored hash to determine authenticity.

### Step 8:
If the hashes match, the certificate is authentic; otherwise, it is not.

## Program:
```
NAME:JEECIKASRINA M
REG NO:212223100015

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
contract CertificateVerification {
address public university;
mapping(bytes32 => bool) public certificates; // Store hashed certificates
event CertificateIssued(bytes32 indexed certHash);
constructor() {
university = msg.sender; // University deploys the contract
}
function issueCertificate(string memory studentName, string memory degree, uint256 year) public {
require(msg.sender == university, "Only university can issue certificates");
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
certificates[certHash] = true;
emit CertificateIssued(certHash);
}
function verifyCertificate(string memory studentName, string memory degree, uint256 year) public view returns (bool) {
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
return certificates[certHash];
}
}
```
# Expected Output:

![block ](https://github.com/user-attachments/assets/cabbd090-0b99-4ead-8836-828bfb486360)

![bb 2](https://github.com/user-attachments/assets/bda9e064-411a-433b-bb6c-b9ce2d2190c5)

![bb](https://github.com/user-attachments/assets/593fe7c7-f0e9-4bdd-bae5-0153585cb834)

● When the university issues a certificate, it gets stored as a hash.
● A student or employer can verify the certificate by entering the details.
● If valid, it returns true; otherwise, false.
High-Level Overview:
● Used to prevent fake certificates.
● Enables quick verification by employers or other institutions.
● Shows how blockchain can be used in education and credential verification.

# Result:
Thus the experiment executed sucessfully.

