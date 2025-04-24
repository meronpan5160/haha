// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;



import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract USDTZ is ERC20Burnable, Ownable {
    uint256 private immutable _cap;

    constructor() ERC20("Tether USD.Z", "USDT.Z") Ownable(msg.sender) {
        _cap = 1_000_000_000 * 10 ** decimals(); // 1 billion tokens
        _mint(msg.sender, _cap / 2); // Mint 50% to the creator
    }

    function cap() public view returns (uint256) {
        return _cap;
    }

    function mint(address to, uint256 amount) public onlyOwner {
        require(totalSupply() + amount <= _cap, "Cap exceeded");
        _mint(to, amount);
    }
}
