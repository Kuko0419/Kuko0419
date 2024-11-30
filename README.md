// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyCustomToken is ERC20 {
    address public owner;

    constructor() ERC20("MyCustomToken", "MCT") {
        owner = msg.sender;
        _mint(msg.sender, 1000000 * 10 ** decimals()); // Mint 1 million tokens to the deployer
    }

    // Custom minting function (only owner can mint new tokens)
    function mint(address to, uint256 amount) external {
        require(msg.sender == owner, "Only the owner can mint");
        _mint(to, amount);
    }

    // Override _transfer for custom behavior (e.g., miner rewards or fees)
    function _transfer(
        address from,
        address to,
        uint256 amount
    ) internal override {
        super._transfer(from, to, amount);
        // Custom logic can be added here (e.g., mint rewards, charge fees)
    }
}
-
