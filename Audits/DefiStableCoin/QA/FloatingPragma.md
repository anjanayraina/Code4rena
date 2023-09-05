# [QA-02] Floating Pragma must be avoided using in the functions 

## Medium Risk 

# Summary

The use of Floating Pragma must be avoided to prevent contracts from accidently getting deployed using an older compiler version with unfixed bugs 

## Impact
some unfixed bugs that might exsit that then hamper the functioning of the deployed contracts 

## Total instances 
https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/blob/main/src/DSCEngine.sol#L201
https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/blob/main/src/DSCEngine.sol#L279

## Tools Used 

- Remix IDE 
- VS Code 
- Solidity Metrics 

## Recommend Mitigation

There are some ways to implement some form of access control on the DecentralizedStableCoin contract and at the same time grant the access to the DSCEngine contract to call burn and mint on DecentralizedStableCoin. 

- Instead of having an onlyOwner modifier , AccessControl library (by OpenZepplin) can be used to grant some addresses the right to mint and burn tokens 
- The DecentralizedStableCoin contract can also be deployed directly from the contructoro of DSCEngine , this will make DSCEngine the owner of the contract hence giving it the power to mint and burn tokens 