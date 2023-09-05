# [NC-01] Missing Validation Checks for tokenA and tokenB in **approveContractToSpend** function 

Since the contract is only dealing with weth and rdpx tokens , so all the transactions that happen must involve those tokens only. Please consider adding a check for checking if the token address passed is either tokenA or tokenB

```  function approveContractToSpend(
    address _token,
    address _spender,
    uint256 _amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
    require(_token == addresses.tokenA || _token ==addresses.tokenB )
    require(_token != address(0), "reLPContract: token cannot be 0");
    require(_spender != address(0), "reLPContract: spender cannot be 0");
    require(_amount > 0, "reLPContract: amount must be greater than 0");
    IERC20WithBurn(_token).approve(_spender, _amount); 

  }
