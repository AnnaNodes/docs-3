---
title: IFtsoRewardManager
---

<!-- This is an autogenerated file. Do not edit! -->

# `IFtsoRewardManager` { #ct_iftsorewardmanager }

<div class="api-node-source" markdown>
[Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)
</div>

<div class="api-node-internal" markdown>

Interface for the [`FtsoRewardManager`](./FtsoRewardManager.md) contract.

</div>

<div class="api-node-type" markdown>

## Events

<div class="api-node" markdown>

### `FeePercentageChanged` { #ev_feepercentagechanged }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event FeePercentageChanged(
    address dataProvider,
    uint256 value,
    uint256 validFromEpoch
)
```

Emitted when a data provider changes its fee.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `dataProvider` | `address` | Address of the data provider. |
| `value` | `uint256` | New fee, in BIPS. |
| `validFromEpoch` | `uint256` | Epoch ID where the new fee takes effect. |

</div>
</div>

<div class="api-node" markdown>

### `FtsoRewardManagerActivated` { #ev_ftsorewardmanageractivated }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event FtsoRewardManagerActivated(
    address ftsoRewardManager
)
```

Emitted when the reward manager contract is activated.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `ftsoRewardManager` | `address` | The reward manager contract. |

</div>
</div>

<div class="api-node" markdown>

### `FtsoRewardManagerDeactivated` { #ev_ftsorewardmanagerdeactivated }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event FtsoRewardManagerDeactivated(
    address ftsoRewardManager
)
```

Emitted when the reward manager contract is deactivated.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `ftsoRewardManager` | `address` | The reward manager contract. |

</div>
</div>

<div class="api-node" markdown>

### `RewardClaimed` { #ev_rewardclaimed }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event RewardClaimed(
    address dataProvider,
    address whoClaimed,
    address sentTo,
    uint256 rewardEpoch,
    uint256 amount
)
```

Emitted when a data provider claims its FTSO rewards.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `dataProvider` | `address` | Address of the data provider that accrued the reward. |
| `whoClaimed` | `address` | Address that actually performed the claim. |
| `sentTo` | `address` | Address that received the reward. |
| `rewardEpoch` | `uint256` | ID of the reward epoch where the reward was accrued. |
| `amount` | `uint256` | Amount of rewarded native tokens (wei). |

</div>
</div>

<div class="api-node" markdown>

### `RewardClaimsEnabled` { #ev_rewardclaimsenabled }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event RewardClaimsEnabled(
    uint256 rewardEpochId
)
```

Emitted when reward claims have been enabled.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `rewardEpochId` | `uint256` | First claimable reward epoch. |

</div>
</div>

<div class="api-node" markdown>

### `RewardClaimsExpired` { #ev_rewardclaimsexpired }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event RewardClaimsExpired(
    uint256 rewardEpochId
)
```

Unclaimed rewards have expired and are now inaccessible.

`getUnclaimedReward()` can be used to retrieve more information.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `rewardEpochId` | `uint256` | ID of the reward epoch that has just expired. |

</div>
</div>

<div class="api-node" markdown>

### `RewardsDistributed` { #ev_rewardsdistributed }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event RewardsDistributed(
    address ftso,
    uint256 epochId,
    address[] addresses,
    uint256[] rewards
)
```

Emitted every price epoch, when rewards have been distributed to each contributing data provider.
Note that rewards are not claimable until the reward epoch finishes.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `ftso` | `address` | Address of the FTSO that generated the rewards. |
| `epochId` | `uint256` | ID of the reward epoch where the rewards were accrued. |
| `addresses` | `address[]` | Data provider addresses that have rewards to claim. |
| `rewards` | `uint256[]` | Amounts available for claiming (wei). |

</div>
</div>

<div class="api-node" markdown>

### `UnearnedRewardsAccrued` { #ev_unearnedrewardsaccrued }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event UnearnedRewardsAccrued(
    uint256 epochId,
    uint256 reward
)
```

Emitted when rewards cannot be distributed during a reward epoch
(for example, because the FTSO went into fallback mode) and they are accrued
for later burning.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `epochId` | `uint256` | ID of the reward epoch where the reward was accrued. |
| `reward` | `uint256` | Total amount of accrued rewards (wei). |

</div>
</div>

</div>

<div class="api-node-type" markdown>

## Functions

<div class="api-node" markdown>

### `active` { #fn_active_02fb0c5e }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function active(
) external view returns (
    bool);
```

Whether rewards can be claimed from this reward manager.

</div>
</div>

<div class="api-node" markdown>

### `autoClaim` { #fn_autoclaim_8dc305fa }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function autoClaim(
    address[] _rewardOwners,
    uint256 _rewardEpoch
) external;
```

Allows claiming rewards simultaneously for a list of reward owners and all unclaimed epochs before the
specified one.

This is meant as a convenience all-in-one reward claiming method to be used both by reward owners and
[registered executors](https://docs.flare.network/tech/automatic-claiming/#registered-claiming-process).
It performs a series of operations, besides claiming rewards:

* If a reward owner has enabled its
[Personal Delegation Account](https://docs.flare.network/tech/personal-delegation-account), rewards are also
claimed for the PDA and the total claimed amount is sent to that PDA.
Otherwise, the claimed amount is sent to the reward owner's account.

* Claimed amount is automatically wrapped through the [`WNat`](./WNat.md) contract.

* If the caller is a registered executor with a non-zero fee, the fee is paid to the executor for each claimed
address.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardOwners` | `address[]` | List of reward owners to claim for. |
| `_rewardEpoch` | `uint256` | Last reward epoch ID to claim for. All previous epochs with pending rewards will be claimed too. |

</div>
</div>

<div class="api-node" markdown>

### `claim` { #fn_claim_b2c12192 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function claim(
    address _rewardOwner,
    address payable _recipient,
    uint256 _rewardEpoch,
    bool _wrap
) external returns (
    uint256 _rewardAmount);
```

Allows the caller to [`claim`](#fn_claim_b2c12192) rewards for a reward owner.
The caller does not have to be the owner of the rewards, but must be approved by the owner to [`claim`](#fn_claim_b2c12192) on his
behalf by using `setClaimExecutors` on the `claimSetupManager`.

This function is intended to be used to [`claim`](#fn_claim_b2c12192) rewards in case of delegation by percentage.
Reverts if `msg.sender` is delegating by amount.

Anybody can call this method, but rewards can only be sent to the reward owner, therefore no funds can be
stolen. However, by limiting the authorized callers, the owner can control the timing of the calls.

When the reward owner is the caller, rewards can be sent to any recipient set by `setAllowedClaimRecipients` on
the `claimSetupManager`.
The reward owner's [Personal Delegation Account](https://docs.flare.network/tech/personal-delegation-account)
is always an authorized recipient.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardOwner` | `address` | Address of the reward owner. |
| `_recipient` | `address payable` | Address to transfer claimed rewards to. |
| `_rewardEpoch` | `uint256` | Last reward epoch to claim for. All previous epochs with pending rewards will be claimed too. |
| `_wrap` | `bool` | Whether claimed rewards should be wrapped through the [`WNat`](./WNat.md) contract before transferring them to the `_recipient`. This parameter is offered as a convenience. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_rewardAmount` | `uint256` | Total amount of claimed rewards (wei). |
</div>
</div>

<div class="api-node" markdown>

### `claimFromDataProviders` { #fn_claimfromdataproviders_21bb25af }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function claimFromDataProviders(
    address _rewardOwner,
    address payable _recipient,
    uint256[] _rewardEpochs,
    address[] _dataProviders,
    bool _wrap
) external returns (
    uint256 _rewardAmount);
```

Allows the caller to [`claim`](#fn_claim_b2c12192) rewards for a reward owner from specific data providers.
The caller does not have to be the owner of the rewards, but must be approved by the owner to [`claim`](#fn_claim_b2c12192) on his
behalf by using `setClaimExecutors` on the `claimSetupManager`.

This function is intended to be used to [`claim`](#fn_claim_b2c12192) rewards in case of delegation by amount (explicit delegation).
Reverts if `msg.sender` is delegating by percentage.

Anybody can call this method, but rewards can only be sent to the reward owner, therefore no funds can be
stolen. However, by limiting the authorized callers, the owner can control the timing of the calls.

When the reward owner is the caller, rewards can be sent to any recipient set by `setAllowedClaimRecipients` on
the `claimSetupManager`.
The reward owner's [Personal Delegation Account](https://docs.flare.network/tech/personal-delegation-account)
is always an authorized recipient.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardOwner` | `address` | Address of the reward owner. |
| `_recipient` | `address payable` | Address to transfer claimed rewards to. |
| `_rewardEpochs` | `uint256[]` | Array of reward epoch IDs to claim for. |
| `_dataProviders` | `address[]` | Array of addresses of the data providers to claim the reward from. |
| `_wrap` | `bool` | Whether claimed rewards should be wrapped through the [`WNat`](./WNat.md) contract before transferring them to the `_recipient`. This parameter is offered as a convenience. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_rewardAmount` | `uint256` | Total amount of claimed rewards (wei). |
</div>
</div>

<div class="api-node" markdown>

### `claimReward` { #fn_claimreward_b2af870a }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function claimReward(
    address payable _recipient,
    uint256[] _rewardEpochs
) external returns (
    uint256 _rewardAmount);
```

Allows a percentage delegator to [`claim`](#fn_claim_b2c12192) rewards.
This function is intended to be used to [`claim`](#fn_claim_b2c12192) rewards in case of delegation by percentage.

**This function is deprecated**: use [`claim`](#fn_claim_b2c12192) instead.

Reverts if `msg.sender` is delegating by amount.
Claims for all unclaimed reward epochs to the 'max(_rewardEpochs)'.
Retained for backward compatibility.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_recipient` | `address payable` | Address to transfer funds to. |
| `_rewardEpochs` | `uint256[]` | Array of reward epoch numbers to claim for. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_rewardAmount` | `uint256` | Amount of total claimed rewards (wei). |
</div>
</div>

<div class="api-node" markdown>

### `claimRewardFromDataProviders` { #fn_claimrewardfromdataproviders_d20bb542 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function claimRewardFromDataProviders(
    address payable _recipient,
    uint256[] _rewardEpochs,
    address[] _dataProviders
) external returns (
    uint256 _rewardAmount);
```

Allows the caller to [`claim`](#fn_claim_b2c12192) rewards from specific data providers.
This function is intended to be used to [`claim`](#fn_claim_b2c12192) rewards in case of delegation by amount.

**This function is deprecated**: use [`claimFromDataProviders`](#fn_claimfromdataproviders_21bb25af) instead.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_recipient` | `address payable` | Address to transfer funds to. |
| `_rewardEpochs` | `uint256[]` | Array of reward epoch numbers to claim for. |
| `_dataProviders` | `address[]` | Array of addresses of the data providers to claim the reward from. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_rewardAmount` | `uint256` | Total amount of claimed rewards (wei). |
</div>
</div>

<div class="api-node" markdown>

### `getClaimedReward` { #fn_getclaimedreward_85b4c538 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getClaimedReward(
    uint256 _rewardEpoch,
    address _dataProvider,
    address _claimer
) external view returns (
    bool _claimed,
    uint256 _amount);
```

Returns information on the rewards accrued by a reward owner from a specific data provider at a specific
reward epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardEpoch` | `uint256` | Reward epoch ID to query. |
| `_dataProvider` | `address` | Address of the data provider to query. |
| `_claimer` | `address` | Address of the reward owner to query. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_claimed` | `bool` | Whether the reward has been claimed or not. |
| `_amount` | `uint256` | Accrued amount in wei. |
</div>
</div>

<div class="api-node" markdown>

### `getCurrentRewardEpoch` { #fn_getcurrentrewardepoch_e7c830d4 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getCurrentRewardEpoch(
) external view returns (
    uint256);
```

Returns the current reward epoch ID.

</div>
</div>

<div class="api-node" markdown>

### `getDataProviderCurrentFeePercentage` { #fn_getdataprovidercurrentfeepercentage_cfbcd25f }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getDataProviderCurrentFeePercentage(
    address _dataProvider
) external view returns (
    uint256 _feePercentageBIPS);
```

Returns the current [fee](https://docs.flare.network/tech/ftso/#rewards) percentage of a data provider.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_dataProvider` | `address` | Address of the queried data provider. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_feePercentageBIPS` | `uint256` | Fee percentage in BIPS. |
</div>
</div>

<div class="api-node" markdown>

### `getDataProviderFeePercentage` { #fn_getdataproviderfeepercentage_961c00ed }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getDataProviderFeePercentage(
    address _dataProvider,
    uint256 _rewardEpoch
) external view returns (
    uint256 _feePercentageBIPS);
```

Returns the [fee](https://docs.flare.network/tech/ftso/#rewards) percentage of a data provider at a
given reward epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_dataProvider` | `address` | Address of the queried data provider. |
| `_rewardEpoch` | `uint256` | Reward epoch ID. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_feePercentageBIPS` | `uint256` | Fee percentage in BIPS. |
</div>
</div>

<div class="api-node" markdown>

### `getDataProviderPerformanceInfo` { #fn_getdataproviderperformanceinfo_eb82dd7f }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getDataProviderPerformanceInfo(
    uint256 _rewardEpoch,
    address _dataProvider
) external view returns (
    uint256 _rewardAmount,
    uint256 _votePowerIgnoringRevocation);
```

Returns information on rewards and vote power of a data provider at a given reward epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardEpoch` | `uint256` | Reward epoch ID. |
| `_dataProvider` | `address` | Address of the data provider to query. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_rewardAmount` | `uint256` | Amount of rewards (wei). |
| `_votePowerIgnoringRevocation` | `uint256` | Vote power, not including revocations. |
</div>
</div>

<div class="api-node" markdown>

### `getDataProviderScheduledFeePercentageChanges` { #fn_getdataproviderscheduledfeepercentagechanges_33b7971e }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getDataProviderScheduledFeePercentageChanges(
    address _dataProvider
) external view returns (
    uint256[] _feePercentageBIPS,
    uint256[] _validFromEpoch,
    bool[] _fixed);
```

Returns the scheduled [fee](https://docs.flare.network/tech/ftso/#rewards) percentage changes for a data
provider.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_dataProvider` | `address` | Address of the queried data provider. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_feePercentageBIPS` | `uint256[]` | Array of fee percentages in BIPS. |
| `_validFromEpoch` | `uint256[]` | Array of block numbers from which the fee settings are effective. |
| `_fixed` | `bool[]` | Array of boolean values indicating whether settings are subject to change or not. |
</div>
</div>

<div class="api-node" markdown>

### `getEpochReward` { #fn_getepochreward_d418634a }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getEpochReward(
    uint256 _rewardEpoch
) external view returns (
    uint256 _totalReward,
    uint256 _claimedReward);
```

Returns information on an epoch's rewards.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardEpoch` | `uint256` | Reward epoch ID. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_totalReward` | `uint256` | Total amount of rewards accrued on that epoch, in wei. |
| `_claimedReward` | `uint256` | Total amount of rewards that have already been claimed, in wei. |
</div>
</div>

<div class="api-node" markdown>

### `getEpochsWithClaimableRewards` { #fn_getepochswithclaimablerewards_0441218e }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getEpochsWithClaimableRewards(
) external view returns (
    uint256 _startEpochId,
    uint256 _endEpochId);
```

Returns the reward epoch range for which rewards can be claimed.
Rewards outside this range are unclaimable, either because they have expired or because the reward epoch is
still ongoing.

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_startEpochId` | `uint256` | The oldest epoch ID that allows reward claiming. |
| `_endEpochId` | `uint256` | The newest epoch ID that allows reward claiming. |
</div>
</div>

<div class="api-node" markdown>

### `getEpochsWithUnclaimedRewards` { #fn_getepochswithunclaimedrewards_b4a2043d }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getEpochsWithUnclaimedRewards(
    address _beneficiary
) external view returns (
    uint256[] _epochIds);
```

Returns the array of claimable epoch IDs for which the rewards of a reward owner have not yet been claimed.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_beneficiary` | `address` | Address of the reward owner to query. Reverts if it uses delegation by amount. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_epochIds` | `uint256[]` | Array of epoch IDs. |
</div>
</div>

<div class="api-node" markdown>

### `getInitialRewardEpoch` { #fn_getinitialrewardepoch_3123b7d8 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getInitialRewardEpoch(
) external view returns (
    uint256);
```

Returns the initial reward epoch ID for this reward manager contract.
This corresponds to the oldest reward epoch with claimable rewards in the previous reward manager when this
one took over.
Set by governance through `setInitialRewardData`.

</div>
</div>

<div class="api-node" markdown>

### `getRewardEpochToExpireNext` { #fn_getrewardepochtoexpirenext_3e7ff857 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getRewardEpochToExpireNext(
) external view returns (
    uint256);
```

Returns the reward epoch that will expire next once a new reward epoch starts.

</div>
</div>

<div class="api-node" markdown>

### `getRewardEpochVotePowerBlock` { #fn_getrewardepochvotepowerblock_f2edab5a }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getRewardEpochVotePowerBlock(
    uint256 _rewardEpoch
) external view returns (
    uint256);
```

Returns the [vote power block](https://docs.flare.network/tech/ftso/#vote-power) of a given reward epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardEpoch` | `uint256` | Reward epoch ID. |

</div>
</div>

<div class="api-node" markdown>

### `getStateOfRewards` { #fn_getstateofrewards_a4472c10 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getStateOfRewards(
    address _beneficiary,
    uint256 _rewardEpoch
) external view returns (
    address[] _dataProviders,
    uint256[] _rewardAmounts,
    bool[] _claimed,
    bool _claimable);
```

Returns the state of rewards for a given address at a specific reward epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_beneficiary` | `address` | Address of the beneficiary to query. It can be a data provider or a delegator, for example.<br>Reverts if the queried address is delegating by amount. |
| `_rewardEpoch` | `uint256` | Reward epoch ID to query. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_dataProviders` | `address[]` | Array of addresses of data providers. |
| `_rewardAmounts` | `uint256[]` | Array of reward amounts received from each provider, in wei. |
| `_claimed` | `bool[]` | Array of boolean values indicating whether each reward has been claimed or not. |
| `_claimable` | `bool` | Boolean value indicating whether rewards are claimable or not. |
</div>
</div>

<div class="api-node" markdown>

### `getStateOfRewardsFromDataProviders` { #fn_getstateofrewardsfromdataproviders_e416b7e1 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function getStateOfRewardsFromDataProviders(
    address _beneficiary,
    uint256 _rewardEpoch,
    address[] _dataProviders
) external view returns (
    uint256[] _rewardAmounts,
    bool[] _claimed,
    bool _claimable);
```

Returns the state of rewards for a given address coming from a specific set of data providers, at a specific
reward epoch.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_beneficiary` | `address` | Address of beneficiary to query. |
| `_rewardEpoch` | `uint256` | Reward epoch ID to query. |
| `_dataProviders` | `address[]` | Array of addresses of the data providers to query. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_rewardAmounts` | `uint256[]` | Array of reward amounts received from each provider, in wei. |
| `_claimed` | `bool[]` | Array of boolean values indicating whether each reward has been claimed or not. |
| `_claimable` | `bool` | Boolean value indicating whether rewards are claimable or not. |
</div>
</div>

<div class="api-node" markdown>

### `nextClaimableRewardEpoch` { #fn_nextclaimablerewardepoch_69b91b59 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function nextClaimableRewardEpoch(
    address _rewardOwner
) external view returns (
    uint256);
```

Returns the next claimable reward epoch for a reward owner.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_rewardOwner` | `address` | Address of the reward owner to query. |

</div>
</div>

<div class="api-node" markdown>

### `setDataProviderFeePercentage` { #fn_setdataproviderfeepercentage_16e69328 }

<div class="api-node-source" markdown>
Defined in `IFtsoRewardManager` ([Docs](./IFtsoRewardManager.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IFtsoRewardManager.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function setDataProviderFeePercentage(
    uint256 _feePercentageBIPS
) external returns (
    uint256 _validFromEpoch);
```

Sets the [fee](https://docs.flare.network/tech/ftso/#rewards) a data provider keeps from all delegations.

Takes effect after `feeValueUpdateOffset` reward epochs have elapsed.

When called multiple times inside the same reward epoch, only the last value remains.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_feePercentageBIPS` | `uint256` | Fee percentage in BIPS. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_validFromEpoch` | `uint256` | Reward epoch number when the new fee percentage will become effective. |
</div>
</div>

</div>

