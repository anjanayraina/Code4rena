# [M-01] Onlyowner modifier prevents DSCEngine contract from minting and buring the tokens 

## Medium Risk 

The functions burn and mint in the DecentralizedStableCoin contract have the Onlyowner modifier , so only the address that deployed the contract can call those functions. But these functions are also called by DSCEngine , now since the DSCEngine contract doesnt deploy the DecentralizedStableCoin contract . This makes the burn and mint functions unusable by DSCEngine . This will make every call to depositCollateralAndMintDsc and redeemCollateralForDsc revert and hence break the functioning 

## Total instances 
https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/blob/main/src/DSCEngine.sol#L201

## Tools Used 

- Remix IDE 
- VS Code 
- Solidity Metrics 

## Recommend Mitigation

There are some ways to implement some form of access control on the DecentralizedStableCoin contract and at the same time grant the access to the DSCEngine contract to call burn and mint on DecentralizedStableCoin. 

- Instead of having an onlyOwner modifier , AccessControl library (by OpenZepplin) can be used to grant some addresses the right to mint and burn tokens 
- The DecentralizedStableCoin contract can also be deployed directly from the contructoro of DSCEngine , this will make DSCEngine the owner of the contract hence giving it the power to mint and burn tokens 