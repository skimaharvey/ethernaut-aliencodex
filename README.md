# Alien Codex

Difficulty 7/10

You've uncovered an Alien contract. Claim ownership to complete the level.

Things that might help

Understanding how array storage works
Understanding ABI specifications
Using a very underhanded approach

# Solution

Mess with the dynamic array storage so that array take up all EVM slots (2 \*\* 256 - 1).

1- Make player contact by calling `make_contact()` function

2- call the `retract()` function so that the array underflows and take up all EVM slots

3- owner is located at the slot(0), call `revise` function as follow:

    `revise(keccak(2 ** 256 - 1 + 1 - uint(1)), playerAddressConvertedTo32bytes)`

# Moral

This level exploits the fact that the EVM doesn't validate an array's ABI-encoded length vs its actual payload. (Not accurate anymore because)

Additionally, it exploits the arithmetic underflow of array length, by expanding the array's bounds to the entire storage area of 2^256. The user is then able to modify all contract storage.

Both vulnerabilities are inspired by 2017's Underhanded coding contest
