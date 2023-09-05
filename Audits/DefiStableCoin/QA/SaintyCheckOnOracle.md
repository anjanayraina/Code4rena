## [QA-01] Some of the sanity checks on the Chainlink Oracle are missing 

## Summary 


## Quality Assurance 

## Impact
Some of the sanity checks on the Chainlink Oracle are not present while getting the price of the tokens . 
This makes that the data that the feed returns as invalid , stale or erreneous in the Oracle 

## Total instances 
https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/blob/main/src/libraries/OracleLib.sol#L27

## Tools Used 

- Remix IDE 
- VS Code 
- Solidity Metrics 

## Recommend Mitigation

There are some ways to implement some form of access control on the DecentralizedStableCoin contract and at the same time grant the access to the DSCEngine contract to call burn and mint on DecentralizedStableCoin. 

- Instead of having an onlyOwner modifier , AccessControl library (by OpenZepplin) can be used to grant some addresses the right to mint and burn tokens 
- The DecentralizedStableCoin contract can also be deployed directly from the contructoro of DSCEngine , this will make DSCEngine the owner of the contract hence giving it the power to mint 