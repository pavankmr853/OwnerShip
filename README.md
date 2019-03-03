pragma solidity >=0.4.2;
contract  ownnership {
    address public owner;
    constructor() public {
        owner = msg.sender;
    }
    modifier onlyOwner() {
        require(msg.sender == owner);
        _;
    }
    function checkOwnner() public view returns(bool) {
        if(msg.sender==owner) {
            return true;
        } else {
            return false;
        }
    }
    function transferOwnership(address newOwner)onlyOwner public {
        owner = newOwner;
    }
}
contract Pause {
    bool public pause;
    constructor() public {
        pause = true;
    }
    modifier ispaused{
        require (pause != true);
        _;
    }
    function unpause() public {
        pause = false;
    }
    function pause1() public {
       pause = true;
    }
}
contract sample is ownnership,Pause {
    uint data;
    string Name;
    function setdata(uint a, string memory b)onlyOwner ispaused public returns(string memory) {
        data = a;
        Name  = b;
    }
    function getdata() public view returns (uint, string memory){
        return (data,Name);
    }
}
