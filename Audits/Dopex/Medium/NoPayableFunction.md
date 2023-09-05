# [M-02] No fallback/recieve but the contract intends to send out ether in **emergencyWithdraw** function 

## Summary

If function **collectFees** requires more gas than the block gas limit to complete its execution, it will inevitably fail. Since in the function collectFees, there is iteration over a dynamic array (**positions_array**), once the array becomes large enough and not enough liquidity is removed, this would make the function **revert** everytime as the gas required would ultimately exceed the max gas limit cost . 

## Impact
The recipient wont be able to **collect the fee** for their positions in the pool as their is only one function in the contract that allows for the withdrawl of the fees 

## Total instances 
https://github.com/code-423n4/2023-08-dopex/blob/main/contracts/decaying-bonds/RdpxDecayingBonds.sol#L98

## Tools Used 

- Remix IDE 
- VS Code 
- Solidity Visual Developer 

## Recommend Mitigation

There are some ways of mitigating this problem : 

- Break down the function of collecting the fee into multiple transactions. For example , add parameters give to adding upper bounds and lower bounds for iterating over the array so that only chuncks of the array can be iterated at a time and not the whole array 

- Implement gas-efficient code and test functions with large inputs to ensure they won’t exceed the block gas limit.