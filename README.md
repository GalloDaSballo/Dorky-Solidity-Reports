# Dorky-Solidity-Reports
List of Solidity Reports that make you look like a dork


## NOTICE

We love you, just understand, you're not impressing anyone with these reports, consider improving your skills to find more impressive findings


## Use call instead of transfer for ERC20 - WRONG

`ERC20(token).transfer` is not the same thing as `payable(token).transfer`

The first is a function with a function selector, the second is a `CALL` with capped gas

Check the bytecode, or run with a debugger and you'll see that they are not the same thing

## Unchecked WETH return value

When a specific token implementation is known, it may be fine not to check it's return value.

This is the case for WETH9, [WETH on mainnet](https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2), this contract will always revert on failur and always returns true.

For this specific contract, as a means to save gas, you can skip using `safeTransfer` and nothing bad will happen, I promise.

Or just run a fuzzer and see for yourself
