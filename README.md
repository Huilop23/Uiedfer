# Uiedfer
dexRouter = IUniswapV2Router02(_routerAddress);
        lpPair = IUniswapV2Factory(dexRouter.factory()).createPair(dexRouter.WETH(), address(this));
        lpPairs[lpPair] = true;
        _allowances[address(this)][address(dexRouter)] = type(uint256).max;

        _isExcludedFromFees[owner()] = true;
        _isExcludedFromFees[address(this)] = true;
        _isExcludedFromFees[_treasuryWallet] = true;
        _isExcludedFromFees[DEAD] = true;

        _liquidityHolders[owner()] = true;
        _liquidityHolders[_treasuryWallet] = true;
        _liquidityHolders[_revenueWallet] = true;

        // Approve the owner for Uniswap, timesaver.
        _approve(_msgSender(), _routerAddress, _tTotal);

        // Event regarding the tTotal transferred to the _msgSender.
        emit Transfer(address(0), _msgSender(), _tTotal);
    }

    receive() external payable {}
