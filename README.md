![state](https://img.shields.io/badge/state-deployed-brightgreen)
![license](https://img.shields.io/badge/license-MIT-blue)

# TEZER

Tezer is the first BEP20 tokens to integrate stable USDT coin and dividends. Simply, buy TEZER and farm USDT with fixed 9% rate!

**Tezer contract** : `0x7182736f5C17330492fBbd559364E4F047455463`

**Dividend tracker** : `0x513C19b28cb8CCb468801d94F6B77AD7a21fAEA2`

**IterableMapping** : `0xfbc6b9dd2f301578593c96433db44eb67b002396`

## Known issues

There is a small isue with code, specifically when setting minimum holdings to receieve rewards is half-broken:

```javascript
function updateMinimumHoldingsForReward(uint256 amount) external onlyOwner {
        require(amount != minimumTokenBalanceForDividends, "TEZER_Dividend_Tracker: Same value");
        emit MinimumTokenBalanceForDividendsUpdated(amount, minimumTokenBalanceForDividends);
        minimumTokenBalanceForDividends = amount;
    }
```

This should be:

```javascript
function updateMinimumHoldingsForReward(uint256 amount) external onlyOwner {
        require(amount != minimumTokenBalanceForDividends, "TEZER_Dividend_Tracker: Same value");
        emit MinimumTokenBalanceForDividendsUpdated(amount, minimumTokenBalanceForDividends);
        minimumTokenBalanceForDividends = amount * (10**18);
    }
```
But this wont harm contract since it is still possible to set this `amount * (10 ** 18)` value manually `amount0000000000...`

----------------------------------------------------------------------------------------------------------------------------

Join our [telegram](https://t.me/TezerToken) for any questions.
