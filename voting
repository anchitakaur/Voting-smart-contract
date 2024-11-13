// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Simple voting contract with a pause mechanism
contract SimpleVoting {
    // Define variables for the contract owner, pause status, and candidates
    address public owner;
    bool public paused;
    
    // Structure to hold candidate data
    struct Candidate {
        uint votes;
    }

    // Mapping to store candidates and votes, using string as candidate name
    mapping(string => Candidate) public candidates;

    // Event to log votes
    event Voted(string candidate, address voter, uint amount);

    // Constructor function to initialize the owner
    constructor() {
        owner = msg.sender;  // Set the owner of the contract to the person who deployed it
        paused = false;  // Initially, contract is not paused
    }

    // Modifier to restrict functions to the owner
    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function");
        _;
    }

    // Modifier to check if contract is paused
    modifier whenNotPaused() {
        require(!paused, "Contract is paused");
        _;
    }

    // Function to add a new candidate
    function addCandidate(string memory _name) public onlyOwner {
        candidates[_name] = Candidate(0);  // Initialize candidate with 0 votes
    }

    // Function to allow voting by sending Ether
    function vote(string memory _candidate) public payable whenNotPaused {
        require(msg.value > 0, "Must send Ether to vote"); // Ensure Ether is sent
        candidates[_candidate].votes += msg.value;  // Increase candidate's votes by Ether sent
        emit Voted(_candidate, msg.sender, msg.value);  // Emit event for the vote
    }

    // Function to pause the contract in case of emergency
    function pause() public onlyOwner {
        paused = true;  // Set the paused status to true
    }

    // Function to resume contract functions
    function unpause() public onlyOwner {
        paused = false;  // Set the paused status to false
    }

    // Function to check votes of a candidate
    function getVotes(string memory _candidate) public view returns (uint) {
        return candidates[_candidate].votes;  // Return the votes for the candidate
    }
}
