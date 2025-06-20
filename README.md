// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MagicContract {
    address public immutable owner;
    uint256 public constant THE_ANSWER = 42;
    string public secretWord = "perjetshmeri";
    
    constructor() {
        owner = msg.sender;
    }
    
    function getAnswer() external pure returns(uint256) {
        return THE_ANSWER;
    }
    
    function createNFT(string memory yourName) external {
        emit NFTCreated(yourName, block.timestamp);
    }
    
    function tryToDestroy(string memory _word) external {
        require(keccak256(abi.encodePacked(_word)) == keccak256(abi.encodePacked(secretWord)), 
            "Fjala e gabuar");
        selfdestruct(payable(owner));
    }
    
    event NFTCreated(string name, uint256 time);
}
