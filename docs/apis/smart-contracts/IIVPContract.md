---
title: IIVPContract
---

<!-- This is an autogenerated file. Do not edit! -->

# `IIVPContract` { #ct_iivpcontract }

<div class="api-node-source" markdown>
[Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol) | Inherits from [IICleanable](./IICleanable.md), [IVPContractEvents](./IVPContractEvents.md)
</div>

<div class="api-node-internal" markdown>

Internal interface for helper contracts handling functionality for an associated [`VPToken`](./VPToken.md).

</div>

<div class="api-node-type" markdown>

## Functions

<div class="api-node" markdown>

### `batchVotePowerOfAt` { #fn_batchvotepowerofat_49e3c7e5 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function batchVotePowerOfAt(
    address[] _owners,
    uint256 _blockNumber
) external view returns (
    uint256[]);
```

Get the vote power of a set of addresses at a given block number.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owners` | `address[]` | The list of addresses being queried. |
| `_blockNumber` | `uint256` | The block number being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256[]` | Vote power of each address at `_blockNumber`, including any delegation received. |
</div>
</div>

<div class="api-node" markdown>

### `cleanupBlockNumber` { #fn_cleanupblocknumber_deea13e7 }

<div class="api-node-source" markdown>
Defined in `IICleanable` ([Docs](./IICleanable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IICleanable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function cleanupBlockNumber(
) external view returns (
    uint256);
```

Get the current cleanup block number set with [`setCleanupBlockNumber`](#fn_setcleanupblocknumber_13de97f5).

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | The currently set cleanup block number. |
</div>
</div>

<div class="api-node" markdown>

### `delegate` { #fn_delegate_6230001a }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function delegate(
    address _from,
    address _to,
    uint256 _balance,
    uint256 _bips
) external;
```

[`Delegate`](#ev_delegate) `_bips` percentage of voting power from a delegator address to a delegatee address.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | The address of the delegator. |
| `_to` | `address` | The address of the delegatee. |
| `_balance` | `uint256` | The delegator's current balance |
| `_bips` | `uint256` | The percentage of voting power to be delegated expressed in basis points (1/100 of one percent). Not cumulative: every call resets the delegation value (and a value of 0 revokes delegation). |

</div>
</div>

<div class="api-node" markdown>

### `delegateExplicit` { #fn_delegateexplicit_404d9e82 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function delegateExplicit(
    address _from,
    address _to,
    uint256 _balance,
    uint256 _amount
) external;
```

Explicitly [`delegate`](#fn_delegate_6230001a) `_amount` tokens of voting power from a delegator address to a delegatee address.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | The address of the delegator. |
| `_to` | `address` | The address of the delegatee. |
| `_balance` | `uint256` | The delegator's current balance. |
| `_amount` | `uint256` | An explicit vote power amount to be delegated. Not cumulative: every call resets the delegation value (and a value of 0 undelegates `_to`). |

</div>
</div>

<div class="api-node" markdown>

### `delegatesOf` { #fn_delegatesof_7de5b8ed }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function delegatesOf(
    address _owner
) external view returns (
    address[] _delegateAddresses,
    uint256[] _bips,
    uint256 _count,
    uint256 _delegationMode);
```

Get the percentages and addresses being delegated to by a vote power delegator.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | The address of the delegator being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_delegateAddresses` | `address[]` | Array of delegatee addresses. |
| `_bips` | `uint256[]` | Array of delegation percents specified in basis points (1/100 or 1 percent), for each delegatee. |
| `_count` | `uint256` | The number of returned delegatees. |
| `_delegationMode` | `uint256` | The mode of the delegation (NOTSET=0, PERCENTAGE=1, AMOUNT=2). See [`Delegatable`](./Delegatable.md).DelegationMode. |
</div>
</div>

<div class="api-node" markdown>

### `delegatesOfAt` { #fn_delegatesofat_ed475a79 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function delegatesOfAt(
    address _owner,
    uint256 _blockNumber
) external view returns (
    address[] _delegateAddresses,
    uint256[] _bips,
    uint256 _count,
    uint256 _delegationMode);
```

Get the percentages and addresses being delegated to by a vote power delegator,
at a given block.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | The address of the delegator being queried. |
| `_blockNumber` | `uint256` | The block number being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| `_delegateAddresses` | `address[]` | Array of delegatee addresses. |
| `_bips` | `uint256[]` | Array of delegation percents specified in basis points (1/100 or 1 percent), for each delegatee. |
| `_count` | `uint256` | The number of returned delegatees. |
| `_delegationMode` | `uint256` | The mode of the delegation (NOTSET=0, PERCENTAGE=1, AMOUNT=2). See [`Delegatable`](./Delegatable.md).DelegationMode. |
</div>
</div>

<div class="api-node" markdown>

### `delegationModeOf` { #fn_delegationmodeof_f6837767 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function delegationModeOf(
    address _who
) external view returns (
    uint256);
```

Get the delegation mode of an address. This mode determines whether vote power is
allocated by percentage or by explicit value and cannot be changed once set with
[`delegate`](#fn_delegate_6230001a) or [`delegateExplicit`](#fn_delegateexplicit_404d9e82).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_who` | `address` | The address being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Delegation mode (NOTSET=0, PERCENTAGE=1, AMOUNT=2). See [`Delegatable`](./Delegatable.md).DelegationMode. |
</div>
</div>

<div class="api-node" markdown>

### `isReplacement` { #fn_isreplacement_aa94d3f2 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function isReplacement(
) external view returns (
    bool);
```

Return true if this [`IIVPContract`](./IIVPContract.md) is configured to be used as a replacement for other contract.
It means that vote powers are not necessarily correct at the initialization, therefore
every method that reads vote power must check whether it is initialized for that address and block.

</div>
</div>

<div class="api-node" markdown>

### `ownerToken` { #fn_ownertoken_65371883 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function ownerToken(
) external view returns (
    contract IVPToken);
```

The [`VPToken`](./VPToken.md) (or some other contract) that owns this [`VPContract`](./VPContract.md).
All state changing methods may be called only from this address.
This is because original `msg.sender` is typically sent in a parameter
and we must make sure that it cannot be faked by directly calling
[`IIVPContract`](./IIVPContract.md) methods.
Owner token is also used in case of replacement to recover vote powers from balances.

</div>
</div>

<div class="api-node" markdown>

### `revokeDelegationAt` { #fn_revokedelegationat_c7c62fab }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function revokeDelegationAt(
    address _from,
    address _to,
    uint256 _balance,
    uint256 _blockNumber
) external;
```

[`Revoke`](#ev_revoke) all vote power delegation from a delegator address to a delegatee address at a given block.
Only affects the reads via [`votePowerOfAtCached`](#fn_votepowerofatcached_e587497e) in the block `_blockNumber`.
This method should be used only to prevent rogue [`delegate`](#fn_delegate_6230001a) voting in the current voting block.
To stop delegating use [`delegate`](#fn_delegate_6230001a) or [`delegateExplicit`](#fn_delegateexplicit_404d9e82) with value of 0,
or [`undelegateAll`](#fn_undelegateall_05109ecf)/ [`undelegateAllExplicit`](#fn_undelegateallexplicit_0f8b8af7).

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | The address of the delegator. |
| `_to` | `address` | Address of the delegatee. |
| `_balance` | `uint256` | The delegator's current balance. |
| `_blockNumber` | `uint256` | The block number at which to revoke delegation. Must be in the past. |

</div>
</div>

<div class="api-node" markdown>

### `setCleanerContract` { #fn_setcleanercontract_f6a494af }

<div class="api-node-source" markdown>
Defined in `IICleanable` ([Docs](./IICleanable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IICleanable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function setCleanerContract(
    address _cleanerContract
) external;
```

Set the contract that is allowed to call history cleaning methods.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_cleanerContract` | `address` | Address of the cleanup contract. Usually this will be an instance of [`CleanupBlockNumberManager`](./CleanupBlockNumberManager.md). |

</div>
</div>

<div class="api-node" markdown>

### `setCleanupBlockNumber` { #fn_setcleanupblocknumber_13de97f5 }

<div class="api-node-source" markdown>
Defined in `IICleanable` ([Docs](./IICleanable.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IICleanable.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function setCleanupBlockNumber(
    uint256 _blockNumber
) external;
```

Set the cleanup block number.
Historic data for the blocks before [`cleanupBlockNumber`](#fn_cleanupblocknumber_deea13e7) can be erased.
History before that block should never be used since it can be inconsistent.
In particular, cleanup block number must be lower than the current vote power block.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_blockNumber` | `uint256` | The new cleanup block number. |

</div>
</div>

<div class="api-node" markdown>

### `undelegateAll` { #fn_undelegateall_05109ecf }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function undelegateAll(
    address _from,
    uint256 _balance
) external;
```

Undelegate all voting power for a delegator address.
Can only be used with percentage delegation.
Does not reset delegation mode back to `NOTSET`.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | The address of the delegator. |
| `_balance` | `uint256` | The delegator's current balance. |

</div>
</div>

<div class="api-node" markdown>

### `undelegateAllExplicit` { #fn_undelegateallexplicit_0f8b8af7 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function undelegateAllExplicit(
    address _from,
    address[] _delegateAddresses
) external returns (
    uint256);
```

Undelegate all explicit vote power by amount for a delegator address.
Can only be used with explicit delegation.
Does not reset delegation mode back to `NOTSET`.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | The address of the delegator. |
| `_delegateAddresses` | `address[]` | Explicit delegation does not store delegatees' addresses, so the caller must supply them. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | The amount still delegated (in case the list of delegates was incomplete). |
</div>
</div>

<div class="api-node" markdown>

### `undelegatedVotePowerOf` { #fn_undelegatedvotepowerof_4a03d556 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function undelegatedVotePowerOf(
    address _owner,
    uint256 _balance
) external view returns (
    uint256);
```

Compute the current undelegated vote power of an address.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | The address being queried. |
| `_balance` | `uint256` | Current balance of that address. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | The unallocated vote power of `_owner`, this is, the amount of vote power currently not being delegated to other addresses. |
</div>
</div>

<div class="api-node" markdown>

### `undelegatedVotePowerOfAt` { #fn_undelegatedvotepowerofat_31503927 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function undelegatedVotePowerOfAt(
    address _owner,
    uint256 _balance,
    uint256 _blockNumber
) external view returns (
    uint256);
```

Compute the undelegated vote power of an address at a given block.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_owner` | `address` | The address being queried. |
| `_balance` | `uint256` |  |
| `_blockNumber` | `uint256` | The block number being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | The unallocated vote power of `_owner`, this is, the amount of vote power that was not being delegated to other addresses at that block number. |
</div>
</div>

<div class="api-node" markdown>

### `updateAtTokenTransfer` { #fn_updateattokentransfer_eadb4362 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function updateAtTokenTransfer(
    address _from,
    address _to,
    uint256 _fromBalance,
    uint256 _toBalance,
    uint256 _amount
) external;
```

Update vote powers when tokens are transferred.
Also update delegated vote powers for percentage delegation
and check for enough funds for explicit delegations.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | Source account of the transfer. |
| `_to` | `address` | Destination account of the transfer. |
| `_fromBalance` | `uint256` | Balance of the source account before the transfer. |
| `_toBalance` | `uint256` | Balance of the destination account before the transfer. |
| `_amount` | `uint256` | Amount that has been transferred. |

</div>
</div>

<div class="api-node" markdown>

### `votePowerFromTo` { #fn_votepowerfromto_9dc6b9f2 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerFromTo(
    address _from,
    address _to,
    uint256 _balance
) external view returns (
    uint256);
```

Get current delegated vote power from a delegator to a delegatee.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | Address of the delegator. |
| `_to` | `address` | Address of the delegatee. |
| `_balance` | `uint256` | The delegator's current balance. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | The delegated vote power. |
</div>
</div>

<div class="api-node" markdown>

### `votePowerFromToAt` { #fn_votepowerfromtoat_833aca92 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerFromToAt(
    address _from,
    address _to,
    uint256 _balance,
    uint256 _blockNumber
) external view returns (
    uint256);
```

Get delegated the vote power from a delegator to a delegatee at a given block number.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_from` | `address` | Address of the delegator. |
| `_to` | `address` | Address of the delegatee. |
| `_balance` | `uint256` | The delegator's current balance. |
| `_blockNumber` | `uint256` | The block number being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | The delegated vote power. |
</div>
</div>

<div class="api-node" markdown>

### `votePowerOf` { #fn_votepowerof_142d1018 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerOf(
    address _who
) external view returns (
    uint256);
```

Get the current vote power of an address.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_who` | `address` | The address being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Current vote power of `_who`, including any delegation received. |
</div>
</div>

<div class="api-node" markdown>

### `votePowerOfAt` { #fn_votepowerofat_92bfe6d8 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerOfAt(
    address _who,
    uint256 _blockNumber
) external view returns (
    uint256);
```

Get the vote power of an address at a given block number

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_who` | `address` | The address being queried. |
| `_blockNumber` | `uint256` | The block number being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Vote power of `_who` at `_blockNumber`, including any delegation received. |
</div>
</div>

<div class="api-node" markdown>

### `votePowerOfAtCached` { #fn_votepowerofatcached_e587497e }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerOfAtCached(
    address _who,
    uint256 _blockNumber
) external returns (
    uint256);
```

Get the vote power of an address at a given block number.
Reads/updates cache and upholds revocations.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_who` | `address` | The address being queried. |
| `_blockNumber` | `uint256` | The block number being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Vote power of `_who` at `_blockNumber`, including any delegation received. |
</div>
</div>

<div class="api-node" markdown>

### `votePowerOfAtIgnoringRevocation` { #fn_votepowerofatignoringrevocation_04bb4e43 }

<div class="api-node-source" markdown>
Defined in `IIVPContract` ([Docs](./IIVPContract.md), [Source](https://gitlab.com/flarenetwork/flare-smart-contracts/-/tree/master/contracts/token/interface/IIVPContract.sol)).
</div>

<div class="api-node-internal" markdown>

```solidity
function votePowerOfAtIgnoringRevocation(
    address _who,
    uint256 _blockNumber
) external view returns (
    uint256);
```

Get the vote power of an address at a given block number, ignoring revocation information and cache.

| Parameters | Type | Description |
| ---------- | ---- | ----------- |
| `_who` | `address` | The address being queried. |
| `_blockNumber` | `uint256` | The block number being queried. |

| Returns | Type | Description |
| ------- | ---- | ----------- |
| [0] | `uint256` | Vote power of `_who` at `_blockNumber`, including any delegation received. Result doesn't change if vote power is revoked. |
</div>
</div>

</div>

