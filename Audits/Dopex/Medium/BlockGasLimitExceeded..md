# [M-01] Block Gas Limit might get Exceeded while collecting fee  

## Summary

If function **collectFees** requires more gas than the block gas limit to complete its execution, it will inevitably fail. Since in the function collectFees, there is iteration over a dynamic array (positions_array), once the array becomes large enough and not enough users remove their liquidity , this would make the function **revert** everytime as the gas required would 

## Impact
The recipient wont be able to collect the fee for their positions in the pool as their is only one function in the contract that allows for the withdrawl of the fees 

## Total instances 
https://github.com/code-423n4/2023-08-dopex/blob/eb4d4a201b3a75dd4bddc74a34e9c42c71d0d12f/contracts/amo/UniV3LiquidityAmo.sol#L119C1-L133C4

## Tools Used 

- Remix IDE 
- VS Code 
- Solidity Metrics 

## Recommend Mitigation

There are some ways to implement some form of access control on the DecentralizedStableCoin contract and at the same time grant the access to the DSCEngine contract to call burn and mint on DecentralizedStableCoin. 

- Instead of having an onlyOwner modifier , AccessControl library (by OpenZepplin) can be used to grant some addresses the right to mint and burn tokens 
- The DecentralizedStableCoin contract can also be deployed directly from the contructoro of DSCEngine , this will make DSCEngine the owner of the contract hence giving it the power to mint and burn tokens 