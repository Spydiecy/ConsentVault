# ConsentVault

ConsentVault is a web-based platform for managing health consents. It allows patients to register, approve consents, and fetch their consent data. Hospitals/clinics can create and fetch consents. The platform is built with HTML, CSS, and JavaScript, and it interacts with a smart contract on the blockchain for managing consents.

## Table of Contents
- [Introduction](#introduction)
- [Mockups](#mockups)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Smart Contract](#smart-contract)

## Introduction

ConsentVault is designed to streamline the process of managing consents in the healthcare industry. It provides a user-friendly interface for patients and healthcare providers to handle consent requests and approvals efficiently.

## Mockups

![image](https://github.com/user-attachments/assets/53d16687-ffd4-4541-b275-0ec185e89ba5)

## Features

1. Register as a patient
   
![image](https://github.com/user-attachments/assets/7d8d965d-71bd-4d2e-818e-71b4f24f1a19)
    

2. Approve consent requests

![image](https://github.com/user-attachments/assets/8c4f9110-7d13-481b-9713-b52377ce1cb8)
    

3. Create consent requests
   
![image](https://github.com/user-attachments/assets/db3d5bac-abd6-428a-ae68-8b16ba78aab4)
    

4.Fetch consent data

![image](https://github.com/user-attachments/assets/cb999ebb-f805-419e-b15c-f92a4d3f8c58)
    

## Technologies Used

- HTML
- CSS
- JavaScript
- Solidity (for the smart contract)
- Web3.js (for interacting with the smart contract)

## Smart Contract
The smart contract is written in Solidity and deployed on the UZH Ethereum blockchain. It manages the following:

1. Patient Smart Contract:
   
   Smart Contract is deployed at: https://uzhethw.ifi.uzh.ch/address/0xe709dDc00378D7A4824FD2b8711D34Ace05F7B40

   ```
   // SPDX-License-Identifier: MIT
   pragma solidity ^0.8.0;
   
   contract Patient {
       struct PatientData {
           uint256 mrn;
           string name;
           string dob;
           string gender;
           string contactInfo;
           string addressInfo;
           uint256 insurancePolicyNumber;
           string generalConsentFormID;
           string proceduralConsentFormID;
           uint256 encounterNumber;
           address hctWalletAddress;
       }
   
       mapping(uint256 => PatientData) public patients;
   
       function registerPatient(
           uint256 _mrn,
           string memory _name,
           string memory _dob,
           string memory _gender,
           string memory _contactInfo,
           string memory _addressInfo,
           uint256 _insurancePolicyNumber,
           string memory _generalConsentFormID,
           string memory _proceduralConsentFormID,
           uint256 _encounterNumber,
           address _hctWalletAddress
       ) public {
           patients[_mrn] = PatientData(
               _mrn,
               _name,
               _dob,
               _gender,
               _contactInfo,
               _addressInfo,
               _insurancePolicyNumber,
               _generalConsentFormID,
               _proceduralConsentFormID,
               _encounterNumber,
               _hctWalletAddress
           );
       }
   
       function getPatient(uint256 _mrn) public view returns (PatientData memory) {
           return patients[_mrn];
       }
   }
   ```

2. Consent Smart Contract:

   Smart Contract is deployed at: https://uzhethw.ifi.uzh.ch/address/0xD0c707a48EF40cdaBBaD6F67157B707f66Ab704A
     
   ```
   // SPDX-License-Identifier: MIT
   pragma solidity ^0.8.0;
   
   contract Consent {
       struct ConsentData {
           uint256 consentID;
           uint256 patientMRN;
           uint256 hospitalID;
           uint256 insuranceID;
           string consentType;
           bool isApproved;
       }
   
       mapping(uint256 => ConsentData) public consents;
   
       function createConsent(
           uint256 _consentID,
           uint256 _patientMRN,
           uint256 _hospitalID,
           uint256 _insuranceID,
           string memory _consentType
       ) public {
           consents[_consentID] = ConsentData(
               _consentID,
               _patientMRN,
               _hospitalID,
               _insuranceID,
               _consentType,
               false
           );
       }
   
       function approveConsent(uint256 _consentID) public {
           consents[_consentID].isApproved = true;
       }
   
       function getConsent(uint256 _consentID) public view returns (ConsentData memory) {
           return consents[_consentID];
       }
   }
   ```
   
   



