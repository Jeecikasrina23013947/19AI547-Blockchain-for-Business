# Experiment 2: Blockchain-Based Crowdfunding (Kickstarter Alternative)
DATE:16.04.2025
## Aim:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

## Algorithm:
### Step 1:
Deploy a smart contract where the project owner sets the funding goal and deadline.

### Step 2:
Define campaign details: project owner address, funding goal, deadline, total contributions, and contributors.

### Step 3:
Contributors send ETH to the campaign, and their contribution is recorded in the contract.

### Step 4:
The smart contract tracks the total ETH raised for the campaign.

### Step 5:
After each contribution, check if the funding goal is met before the deadline.

### Step 6:
If the goal is met before the deadline, release funds to the project owner. If the goal isn’t met before the deadline, allow contributors to withdraw their funds.

### Step 7:
Contributors can withdraw their funds if the goal was not met.

### Step 8:
Once the deadline passes, the campaign ends, and either funds are released to the owner or refunded to contributors.

## Program:
NAME:JEECIKASRINA M
REG:212223100015
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```
# Expected Output:

![exp 02](https://github.com/user-attachments/assets/f87a27f2-ec88-48de-8c9e-99ed6c42c1b0)

![WhatsApp Image 2025-04-16 at 21 05 23_5a06b3e1](https://github.com/user-attachments/assets/24096287-ec4e-43cd-b96d-f695f17174b9)

![mm](https://github.com/user-attachments/assets/1c02ff50-52bb-4256-a087-4b85662ef1fa)


Users can contribute ETH to the campaign.


If the goal is met, the creator can withdraw funds.


If the goal is not met, contributors can claim a refund.


# High-Level Overview:
Teaches decentralized fundraising.


Avoids fraud by ensuring funds are only transferred if the goal is met.

# RESULT: 
Thus the experiment successfully executed.
