---
title: IFtso
---

<!-- This is an autogenerated file. Do not edit! -->

# `IFtso` { #ct_iftso }

<div class="api-node-source" markdown>
[Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)
</div>

<div class="api-node-internal" markdown>

Interface for each of the FTSO contracts that handles an asset.
Read the [FTSO documentation page](https://docs.flare.network/tech/ftso/)
for general information about the FTSO system.

</div>

<div class="api-node-type" markdown>

## Enums

<div class="api-node" markdown>

### `PriceFinalizationType` { #en_pricefinalizationtype }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

</div>
```solidity
enum PriceFinalizationType {
  NOT_FINALIZED,
  WEIGHTED_MEDIAN,
  TRUSTED_ADDRESSES,
  PREVIOUS_PRICE_COPIED,
  TRUSTED_ADDRESSES_EXCEPTION,
  PREVIOUS_PRICE_COPIED_EXCEPTION
}
```

How did a price epoch finalize.

* `NOT_FINALIZED`: The epoch has not been finalized yet. This is the initial state.
* `WEIGHTED_MEDIAN`: The median was used to calculate the final price.
    This is the most common state in normal operation.
* `TRUSTED_ADDRESSES`: Due to low turnout, the final price was calculated using only
    the median of trusted addresses.
* `PREVIOUS_PRICE_COPIED`: Due to low turnout and absence of votes from trusted addresses,
    the final price was copied from the previous epoch.
* `TRUSTED_ADDRESSES_EXCEPTION`: Due to an exception, the final price was calculated
    using only the median of trusted addresses.
* `PREVIOUS_PRICE_COPIED_EXCEPTION`: Due to an exception, the final price was copied
    from the previous epoch.

</div>

</div>

<div class="api-node-type" markdown>

## Events

<div class="api-node" markdown>

### `LowTurnout` { #ev_lowturnout }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event LowTurnout(
    uint256 epochId,
    uint256 natTurnout,
    uint256 lowNatTurnoutThresholdBIPS,
    uint256 timestamp
)
```

Not enough votes were received for this asset during a price epoch that has just ended.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `epochId` | `uint256` | The ID of the epoch. |
| `natTurnout` | `uint256` | Total received vote power, as a percentage of the circulating supply in BIPS. |
| `lowNatTurnoutThresholdBIPS` | `uint256` | Minimum required vote power, as a percentage of the circulating supply in BIPS. The fact that this number is higher than `natTurnout` is what triggered this event. |
| `timestamp` | `uint256` | Timestamp of the block where the price epoch ended. |

</div>
</div>

<div class="api-node" markdown>

### `PriceEpochInitializedOnFtso` { #ev_priceepochinitializedonftso }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event PriceEpochInitializedOnFtso(
    uint256 epochId,
    uint256 endTime,
    uint256 timestamp
)
```

All necessary parameters have been set for an epoch and prices can start being _revealed_.
Note that prices can already be _submitted_ immediately after the previous price epoch submit end time is over.

This event is not emitted in fallback mode (see [`getPriceEpochData`](#fn_getpriceepochdata_e3b3a3b3)).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `epochId` | `uint256` | The ID of the epoch that has just started. |
| `endTime` | `uint256` | Deadline to submit prices, in seconds since UNIX epoch. |
| `timestamp` | `uint256` | Current on-chain timestamp. |

</div>
</div>

<div class="api-node" markdown>

### `PriceFinalized` { #ev_pricefinalized }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event PriceFinalized(
    uint256 epochId,
    uint256 price,
    bool rewardedFtso,
    uint256 lowIQRRewardPrice,
    uint256 highIQRRewardPrice,
    uint256 lowElasticBandRewardPrice,
    uint256 highElasticBandRewardPrice,
    enum IFtso.PriceFinalizationType finalizationType,
    uint256 timestamp
)
```

An epoch has ended and the asset price is available.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `epochId` | `uint256` | The ID of the epoch that has just ended. |
| `price` | `uint256` | The asset's price for that epoch. |
| `rewardedFtso` | `bool` | Whether the next 4 parameters contain data. |
| `lowIQRRewardPrice` | `uint256` | Lowest price in the primary (inter-quartile) reward band. |
| `highIQRRewardPrice` | `uint256` | Highest price in the primary (inter-quartile) reward band. |
| `lowElasticBandRewardPrice` | `uint256` | Lowest price in the secondary (elastic) reward band. |
| `highElasticBandRewardPrice` | `uint256` | Highest price in the secondary (elastic) reward band. |
| `finalizationType` | `enum IFtso.PriceFinalizationType` | Reason for the finalization of the epoch. |
| `timestamp` | `uint256` | Timestamp of the block where the price has been finalized. |

</div>
</div>

<div class="api-node" markdown>

### `PriceRevealed` { #ev_pricerevealed }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event PriceRevealed(
    address voter,
    uint256 epochId,
    uint256 price,
    uint256 timestamp,
    uint256 votePowerNat,
    uint256 votePowerAsset
)
```

A voter has revealed its price.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `voter` | `address` | The voter. |
| `epochId` | `uint256` | The ID of the epoch for which the price has been revealed. |
| `price` | `uint256` | The revealed price. |
| `timestamp` | `uint256` | Timestamp of the block where the reveal happened. |
| `votePowerNat` | `uint256` | Vote power of the voter in this epoch. This includes the vote power derived from its [`WNat`](./WNat.md) holdings and the delegations. |
| `votePowerAsset` | `uint256` | _Unused_. |

</div>
</div>

</div>

<div class="api-node-type" markdown>

## Functions

<div class="api-node" markdown>

### `active` { #fn_active_02fb0c5e }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function active(
) external view returns (
    bool);
```

Returns whether FTSO is [`active`](#fn_active_02fb0c5e) or not.

</div>
</div>

<div class="api-node" markdown>

### `getCurrentEpochId` { #fn_getcurrentepochid_a29a839f }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentEpochId(
) external view returns (
    uint256);
```

Returns the current epoch ID.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Currently running epoch ID. IDs are consecutive numbers starting from zero. |
</div>
</div>

<div class="api-node" markdown>

### `getCurrentPrice` { #fn_getcurrentprice_eb91d37e }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentPrice(
) external view returns (
    uint256 _price,
    uint256 _timestamp);
```

Returns the current asset price.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_price` | `uint256` | Price in USD multiplied by 10^`ASSET_PRICE_USD_DECIMALS`. |
| `_timestamp` | `uint256` | Time when price was updated for the last time, in seconds from UNIX epoch. |
</div>
</div>

<div class="api-node" markdown>

### `getCurrentPriceDetails` { #fn_getcurrentpricedetails_040d73b8 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentPriceDetails(
) external view returns (
    uint256 _price,
    uint256 _priceTimestamp,
    enum IFtso.PriceFinalizationType _priceFinalizationType,
    uint256 _lastPriceEpochFinalizationTimestamp,
    enum IFtso.PriceFinalizationType _lastPriceEpochFinalizationType);
```

Returns asset's current price details.
All timestamps are in seconds from UNIX epoch.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_price` | `uint256` | Price in USD multiplied by 10^`ASSET_PRICE_USD_DECIMALS`. |
| `_priceTimestamp` | `uint256` | Time when price was updated for the last time. |
| `_priceFinalizationType` | `enum IFtso.PriceFinalizationType` | Finalization type when price was updated for the last time. |
| `_lastPriceEpochFinalizationTimestamp` | `uint256` | Time when last price epoch was finalized. |
| `_lastPriceEpochFinalizationType` | `enum IFtso.PriceFinalizationType` | Finalization type of last finalized price epoch. |
</div>
</div>

<div class="api-node" markdown>

### `getCurrentPriceFromTrustedProviders` { #fn_getcurrentpricefromtrustedproviders_af52df08 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentPriceFromTrustedProviders(
) external view returns (
    uint256 _price,
    uint256 _timestamp);
```

Returns current asset price calculated only using input from trusted providers.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_price` | `uint256` | Price in USD multiplied by 10^`ASSET_PRICE_USD_DECIMALS`. |
| `_timestamp` | `uint256` | Time when price was updated for the last time, in seconds from UNIX epoch. |
</div>
</div>

<div class="api-node" markdown>

### `getCurrentPriceWithDecimals` { #fn_getcurrentpricewithdecimals_65f5cd86 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentPriceWithDecimals(
) external view returns (
    uint256 _price,
    uint256 _timestamp,
    uint256 _assetPriceUsdDecimals);
```

Returns current asset price and number of decimals.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_price` | `uint256` | Price in USD multiplied by 10^`_assetPriceUsdDecimals`. |
| `_timestamp` | `uint256` | Time when price was updated for the last time, in seconds from UNIX epoch. |
| `_assetPriceUsdDecimals` | `uint256` | Number of decimals used to return the USD price. |
</div>
</div>

<div class="api-node" markdown>

### `getCurrentPriceWithDecimalsFromTrustedProviders` { #fn_getcurrentpricewithdecimalsfromtrustedproviders_3cacb3ae }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentPriceWithDecimalsFromTrustedProviders(
) external view returns (
    uint256 _price,
    uint256 _timestamp,
    uint256 _assetPriceUsdDecimals);
```

Returns current asset price calculated only using input from trusted providers and number of decimals.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_price` | `uint256` | Price in USD multiplied by 10^`ASSET_PRICE_USD_DECIMALS`. |
| `_timestamp` | `uint256` | Time when price was updated for the last time, in seconds from UNIX epoch. |
| `_assetPriceUsdDecimals` | `uint256` | Number of decimals used to return the USD price. |
</div>
</div>

<div class="api-node" markdown>

### `getCurrentRandom` { #fn_getcurrentrandom_d89601fd }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentRandom(
) external view returns (
    uint256);
```

Returns the random number for the previous price epoch, obtained from the random numbers
provided by all data providers along with their data submissions.

</div>
</div>

<div class="api-node" markdown>

### `getEpochId` { #fn_getepochid_5303548b }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getEpochId(
    uint256 _timestamp
) external view returns (
    uint256);
```

Returns the ID of the epoch that was opened for price submission at the specified timestamp.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_timestamp` | `uint256` | Queried timestamp in seconds from UNIX epoch. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Epoch ID corresponding to that timestamp. IDs are consecutive numbers starting from zero. |
</div>
</div>

<div class="api-node" markdown>

### `getEpochPrice` { #fn_getepochprice_7d1d6f12 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getEpochPrice(
    uint256 _epochId
) external view returns (
    uint256);
```

Returns agreed asset price in the specified epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_epochId` | `uint256` | ID of the epoch. Only the last 200 epochs can be queried. Out-of-bounds queries revert. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Price in USD multiplied by 10^`ASSET_PRICE_USD_DECIMALS`. |
</div>
</div>

<div class="api-node" markdown>

### `getEpochPriceForVoter` { #fn_getepochpriceforvoter_c5d8b9e7 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getEpochPriceForVoter(
    uint256 _epochId,
    address _voter
) external view returns (
    uint256);
```

Returns asset price submitted by a voter in the specified epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_epochId` | `uint256` | ID of the epoch being queried. Only the last 200 epochs can be queried. Out-of-bounds queries revert. |
| `_voter` | `address` | Address of the voter being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Price in USD multiplied by 10^`ASSET_PRICE_USD_DECIMALS`. |
</div>
</div>

<div class="api-node" markdown>

### `getPriceEpochConfiguration` { #fn_getpriceepochconfiguration_144e1591 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getPriceEpochConfiguration(
) external view returns (
    uint256 _firstEpochStartTs,
    uint256 _submitPeriodSeconds,
    uint256 _revealPeriodSeconds);
```

Returns current epoch's configuration.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_firstEpochStartTs` | `uint256` | First epoch start timestamp in seconds from UNIX epoch. |
| `_submitPeriodSeconds` | `uint256` | Submit period in seconds. |
| `_revealPeriodSeconds` | `uint256` | Reveal period in seconds. |
</div>
</div>

<div class="api-node" markdown>

### `getPriceEpochData` { #fn_getpriceepochdata_e3b3a3b3 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getPriceEpochData(
) external view returns (
    uint256 _epochId,
    uint256 _epochSubmitEndTime,
    uint256 _epochRevealEndTime,
    uint256 _votePowerBlock,
    bool _fallbackMode);
```

Returns current epoch data.
Intervals are open on the right: End times are not included.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_epochId` | `uint256` | Current epoch ID. |
| `_epochSubmitEndTime` | `uint256` | End time of the price submission window in seconds from UNIX epoch. |
| `_epochRevealEndTime` | `uint256` | End time of the price reveal window in seconds from UNIX epoch. |
| `_votePowerBlock` | `uint256` | Vote power block for the current epoch. |
| `_fallbackMode` | `bool` | Whether the current epoch is in fallback mode. Only votes from trusted addresses are used in this mode. |
</div>
</div>

<div class="api-node" markdown>

### `getRandom` { #fn_getrandom_cd4b6914 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getRandom(
    uint256 _epochId
) external view returns (
    uint256);
```

Returns the random number used in a specific past epoch, obtained from the random numbers
provided by all data providers along with their data submissions.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_epochId` | `uint256` | ID of the queried epoch. Current epoch cannot be queried, and the previous epoch is constantly updated as data providers reveal their prices and random numbers. Only the last 50 epochs can be queried and there is no bounds checking for this parameter. Out-of-bounds queries return undefined values. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | The random number used in that epoch. |
</div>
</div>

<div class="api-node" markdown>

### `symbol` { #fn_symbol_95d89b41 }

<div class="api-node-source" markdown>
Defined in `IFtso` ([Docs](./IFtso.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtso.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function symbol(
) external view returns (
    string);
```

Returns the FTSO [`symbol`](#fn_symbol_95d89b41).

</div>
</div>

</div>

