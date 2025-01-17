---
title: Delegatable
---

<!-- This is an autogenerated file. Do not edit! -->

# `Delegatable` { #ct_delegatable }

<div class="api-node-source" markdown>
[Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol) | Inherits from [IVPContractEvents](./IVPContractEvents.md)
</div>

<div class="api-node-internal" markdown>

[`Delegatable`](./Delegatable.md) ERC20 behavior.

Adds delegation capabilities to tokens. This contract orchestrates interaction between
managing a delegation and the vote power allocations that result.

</div>

<div class="api-node-type" markdown>

## Enums

<div class="api-node" markdown>

### `DelegationMode` { #en_delegationmode }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

</div>
```solidity
enum DelegationMode {
  NOTSET,
  PERCENTAGE,
  AMOUNT
}
```

Delegation mode of an account. Once set, it cannot be changed.

* `NOTSET`: Delegation mode not set yet.
* `PERCENTAGE`: Delegation by percentage.
* `AMOUNT`: Delegation by amount (explicit).

</div>

</div>

<div class="api-node-type" markdown>

## Events

<div class="api-node" markdown>

### `CreatedVotePowerCache` { #ev_createdvotepowercache }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event CreatedVotePowerCache(
    address _owner,
    uint256 _blockNumber
)
```

Emitted when a vote power cache entry is created.
Allows history cleaners to track vote power cache cleanup opportunities off-chain.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | The address whose vote power has just been cached. |
| `_blockNumber` | `uint256` | The block number at which the vote power has been cached. |

</div>
</div>

<div class="api-node" markdown>

### `Delegate` { #ev_delegate }

<div class="api-node-source" markdown>
Defined in `IVPContractEvents` ([Docs](./IVPContractEvents.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IVPContractEvents.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event Delegate(
    address from,
    address to,
    uint256 priorVotePower,
    uint256 newVotePower
)
```

Emitted when the amount of vote power delegated from one account to another changes.

**Note**: This event is always emitted from [`VPToken`](./VPToken.md)'s `writeVotePowerContract`.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `from` | `address` | The account that has changed the amount of vote power it is delegating. |
| `to` | `address` | The account whose received vote power has changed. |
| `priorVotePower` | `uint256` | The vote power originally delegated. |
| `newVotePower` | `uint256` | The new vote power that triggered this event. It can be 0 if the delegation is completely canceled. |

</div>
</div>

<div class="api-node" markdown>

### `Revoke` { #ev_revoke }

<div class="api-node-source" markdown>
Defined in `IVPContractEvents` ([Docs](./IVPContractEvents.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/userInterfaces/IVPContractEvents.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
event Revoke(
    address delegator,
    address delegatee,
    uint256 votePower,
    uint256 blockNumber
)
```

Emitted when an account revokes its vote power delegation to another account
for a single current or past block (typically the current vote block).

**Note**: This event is always emitted from [`VPToken`](./VPToken.md)'s `writeVotePowerContract` or `readVotePowerContract`.

See `revokeDelegationAt` in [`IVPToken`](./IVPToken.md).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `delegator` | `address` | The account that revoked the delegation. |
| `delegatee` | `address` | The account that has been revoked. |
| `votePower` | `uint256` | The revoked vote power. |
| `blockNumber` | `uint256` | The block number at which the delegation has been revoked. |

</div>
</div>

</div>

<div class="api-node-type" markdown>

## Functions

<div class="api-node" markdown>

### `explicitDelegationHistoryCleanup` { #fn_explicitdelegationhistorycleanup_cabc4528 }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function explicitDelegationHistoryCleanup(
    address _from,
    address _to,
    uint256 _count
) external returns (
    uint256);
```

Delete explicit delegation checkpoints that expired (i.e. are before `cleanupBlockNumber`).
Method can only be called from the [`cleanerContract`](#va_cleanercontract) (which may be a proxy to external cleaners).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | Delegator address. |
| `_to` | `address` | Delegatee address. |
| `_count` | `uint256` | Maximum number of checkpoints to delete. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Number of checkpoints deleted. |
</div>
</div>

<div class="api-node" markdown>

### `percentageDelegationHistoryCleanup` { #fn_percentagedelegationhistorycleanup_7f57d58f }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function percentageDelegationHistoryCleanup(
    address _owner,
    uint256 _count
) external returns (
    uint256);
```

Delete percentage delegation checkpoints that expired (i.e. are before `cleanupBlockNumber`).
Method can only be called from the [`cleanerContract`](#va_cleanercontract) (which may be a proxy to external cleaners).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | Balance owner account address. |
| `_count` | `uint256` | Maximum number of checkpoints to delete. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Number of deleted checkpoints. |
</div>
</div>

<div class="api-node" markdown>

### `revocationCleanup` { #fn_revocationcleanup_8c0b6b40 }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function revocationCleanup(
    address _from,
    address _to,
    uint256 _blockNumber
) external returns (
    uint256);
```

Delete revocation entry that expired (i.e. is before `cleanupBlockNumber`).
Method can only be called from the [`cleanerContract`](#va_cleanercontract) (which may be a proxy to external cleaners).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | Delegator address. |
| `_to` | `address` | Delegatee address. |
| `_blockNumber` | `uint256` | Block number for which total supply value was cached. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Number of revocation entries deleted (always 0 or 1). |
</div>
</div>

<div class="api-node" markdown>

### `votePowerCacheCleanup` { #fn_votepowercachecleanup_891339a8 }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerCacheCleanup(
    address _owner,
    uint256 _blockNumber
) external returns (
    uint256);
```

Delete vote power cache entry that expired (i.e. is before `cleanupBlockNumber`).
Method can only be called from the [`cleanerContract`](#va_cleanercontract) (which may be a proxy to external cleaners).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | Vote power owner account address. |
| `_blockNumber` | `uint256` | Block number for which total supply value was cached. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Number of deleted cache entries (always 0 or 1). |
</div>
</div>

<div class="api-node" markdown>

### `votePowerHistoryCleanup` { #fn_votepowerhistorycleanup_1a05274c }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerHistoryCleanup(
    address _owner,
    uint256 _count
) external returns (
    uint256);
```

Delete vote power checkpoints that expired (i.e. are before `cleanupBlockNumber`).
Method can only be called from the [`cleanerContract`](#va_cleanercontract) (which may be a proxy to external cleaners).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | Vote power owner account address. |
| `_count` | `uint256` | Maximum number of checkpoints to delete. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Number of deleted checkpoints. |
</div>
</div>

</div>

<div class="api-node-type" markdown>

## Modifiers

<div class="api-node" markdown>

### `notBeforeCleanupBlock` { #md_notbeforecleanupblock }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
modifier notBeforeCleanupBlock(    uint256 _blockNumber)
```

Reading from history is not allowed before `cleanupBlockNumber`, since data before that
might have been deleted and is thus unreliable.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_blockNumber` | `uint256` | The block number being checked for validity. |

</div>
</div>

<div class="api-node" markdown>

### `onlyCleaner` { #md_onlycleaner }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
modifier onlyCleaner()
```

History cleaning methods can be called only from [`cleanerContract`](#va_cleanercontract).

</div>
</div>

</div>

<div class="api-node-type" markdown>

## Variables

<div class="api-node" markdown>

### `cleanerContract` { #va_cleanercontract }

<div class="api-node-source" markdown>
Defined in `Delegatable` ([Docs](./Delegatable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/implementation/Delegatable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
    address cleanerContract
```

Address of the contract that is allowed to call methods for history cleaning.

</div>
</div>

</div>

