# Errors

In case NIS encounters an error while processing a request it returns an error.

This chapter describes the error messages that can be returned from NIS.

## Error messages



**Request method 'GET' not supported**

The request was performed as a GET request but was expected to be a POST request.


**address must be valid:**

At least one address supplied in the request was invalid. Addresses are validated before processing a request. If validation fails, an error containing this message is returned.


**FAILURE_SERVER_LIMIT:**

The number of accounts that are allowed to harvest on NIS was exceeded.


**JSON Object was expected:**

A parameter is missing in the request.


**FAILURE_UNKNOWN_ACCOUNT:**

The account specified in the request is not known.


**block not found in the db**

The block that was requested could not be found in the database.


**height must be positive**

The block height supplied in a request was zero or negative. Block height must always be greater than zero.


**network has not been booted yet**

Most requests need the node that should answer the request to be already booted. If node is not booted yet, this error message will be returned.


**network boot was already attempted**

It was attempted to boot an already booted node. Nodes can only be booted once.


**remote 123.45.67.89 attempted to call local /node/boot**

It was attempted to boot a remote node. Only local node can be booted.


**FAILURE_PAST_DEADLINE**

The deadline for the entity has already expired. The deadline must always lie in the future.


**FAILURE_FUTURE_DEADLINE**

The deadline lies too far in the future. Deadlines are only allowed to lie up to 24 hours in the future.


**FAILURE_INSUFFICIENT_BALANCE**

The account does not have enough funds.


**FAILURE_MESSAGE_TOO_LARGE**

The message for the transaction exceeds the limit of 512 bytes.


**FAILURE_HASH_EXISTS**

The hash of the entity already exists either in the cache or in the database.


**FAILURE_SIGNATURE_NOT_VERIFIABLE**

The signature of the entity failed upon verification.


**FAILURE_TIMESTAMP_TOO_FAR_IN_PAST**

The timestamp of the entity lies to far in the past.


**FAILURE_TIMESTAMP_TOO_FAR_IN_FUTURE**

The timestamp of the entity lies too far in the future.


**FAILURE_INELIGIBLE_BLOCK_SIGNER**

Validation failed because the block had an ineligible signer. This usually occurs when remote harvesting is in the process of being activated or deactivated.


**FAILURE_ENTITY_UNUSABLE_OUT_OF_SYNC**

The entity cannot be processed because the remote node is out of synchronization with the local node. This happens frequently when a node is not fully synchronized and receives a new block with much larger height than its own chain.


**FAILURE_INSUFFICIENT_FEE**

The supplied transaction has an insufficient fee.


**FAILURE_NEMESIS_ACCOUNT_TRANSACTION_AFTER_NEMESIS_BLOCK**

The supplied transaction has the nemesis account as sender and cannot be included in a normal block.


**FAILURE_TRANSACTION_CACHE_TOO_FULL**

The transaction was rejected because the transaction cache is too full. This happens when an account tries to send too many transactions in a short time. To improve the chance that the transaction gets accepted you can try to raise the transaction fee.


**FAILURE_WRONG_NETWORK**

Entity was rejected because it has the wrong network specified.


**FAILURE_CANNOT_HARVEST_FROM_BLOCKED_ACCOUNT**

Block was rejected because it was harvested by a blocked account (typically a reserved NEM fund).


**FAILURE_DESTINATION_ACCOUNT_HAS_NONZERO_BALANCE**

The importance cannot be transferred to an account with nonzero balance.


**FAILURE_IMPORTANCE_TRANSFER_IN_PROGRESS**

The transaction is conflicting because there is already a transfer of importance in progress.


**FAILURE_IMPORTANCE_TRANSFER_NEEDS_TO_BE_DEACTIVATED**

The transaction is conflicting because the importance was already transferred.


**FAILURE_IMPORTANCE_TRANSFER_IS_NOT_ACTIVE**

The transaction is conflicting because no importance has been transferred yet.


**FAILURE_TRANSACTION_NOT_ALLOWED_FOR_REMOTE**

Validation failed because transaction is using remote account in an improper way.


**FAILURE_MULTISIG_NOT_A_COSIGNER**

The multisig transaction was rejected because the signer of the transaction is not a cosignatory of the sender account of the inner transaction.


**FAILURE_MULTISIG_INVALID_COSIGNERS**

Validation failed because the cosignatories attached to a multisig transaction were invalid.


**FAILURE_MULTISIG_NO_MATCHING_MULTISIG**

The signature transaction was rejected because the corresponding multisig transaction was not found.


**FAILURE_TRANSACTION_NOT_ALLOWED_FOR_MULTISIG**

The transaction was rejected because the signer is a multisig account. Multisig accounts are not allowed to initiate any transaction (only cosignatories are allowed to do so).


**FAILURE_MULTISIG_ALREADY_A_COSIGNER**

The transaction was rejected because it tried to add a cosignatory to a multisig account which already has this cosignatory.


**FAILURE_MULTISIG_MODIFICATION_MULTIPLE_DELETES**

The transaction was rejected because it tried to remove multiple cosignatories at once. It is only allowed to remove one cosignatory at a time.


**FAILURE_MULTISIG_MODIFICATION_REDUNDANT_MODIFICATIONS**

The transaction was rejected because it tried to do redundant modifications. This can happen if a transaction tries to add the same cosignatory two time.


**FAILURE_CONFLICTING_MULTISIG_MODIFICATION**

The transaction was rejected because it contained conflicting modifications to a multisig account. This can for instance happen if a transaction tries to add and then delete the same cosignatory.


**FAILURE_TOO_MANY_MULTISIG_COSIGNERS**

The transaction was rejected because it contains too many cosignatories. The maximum number of cosignatories allowed for a multisig account is 32.


**FAILURE_MULTISIG_ACCOUNT_CANNOT_BE_COSIGNER**

Validation failed because a multisig modification would result in a multisig account being a cosigner.


**FAILURE_MULTISIG_MIN_COSIGNATORIES_OUT_OF_RANGE**

Validation failed because the minimum number of cosignatories is negative or larger than the number of cosignatories.


**FAILURE_NAMESPACE_UNKNOWN**

Validation failed because the namespace is unknown.


**FAILURE_NAMESPACE_ALREADY_EXISTS**

Validation failed because the namespace already exists.


**FAILURE_NAMESPACE_EXPIRED**

Validation failed because the namespace has expired.


**FAILURE_NAMESPACE_OWNER_CONFLICT**

Validation failed because the transaction signer is not the owner of the namespace.


**FAILURE_NAMESPACE_INVALID_NAME(**

Validation failed because the name for the namespace is invalid.


**FAILURE_NAMESPACE_INVALID_RENTAL_FEE_SINK**

Validation failed because the specified namespace rental fee sink is invalid.


**FAILURE_NAMESPACE_INVALID_RENTAL_FEE**

Validation failed because the specified rental fee is invalid.


**FAILURE_NAMESPACE_PROVISION_TOO_EARLY**

Validation failed because the provision was done too early.


**FAILURE_NAMESPACE_NOT_CLAIMABLE**

Validation failed because the namespace contains a reserved part and is not claimable.


**FAILURE_MOSAIC_UNKNOWN**

Validation failed because the mosaic is unknown.


**FAILURE_MOSAIC_MODIFICATION_NOT_ALLOWED**

Validation failed because the modification of the existing mosaic is not allowed.


**FAILURE_MOSAIC_CREATOR_CONFLICT**

Validation failed because the transaction signer is not the creator of the mosaic.


**FAILURE_MOSAIC_SUPPLY_IMMUTABLE**

Validation failed because the mosaic supply is immutable.


**FAILURE_MOSAIC_MAX_SUPPLY_EXCEEDED**

Validation failed because the maximum overall mosaic supply is exceeded.


**FAILURE_MOSAIC_SUPPLY_NEGATIVE**

Validation failed because the resulting mosaic supply would be negative.


**FAILURE_MOSAIC_NOT_TRANSFERABLE**

Validation failed because the mosaic is not transferable.


**FAILURE_MOSAIC_DIVISIBILITY_VIOLATED**

Validation failed because the divisibility of the mosaic is violated.


**FAILURE_CONFLICTING_MOSAIC_CREATION**

Validation failed because conflicting mosaic creation is present.


**FAILURE_MOSAIC_INVALID_CREATION_FEE_SINK**

Validation failed because the mosaic creation fee sink is invalid.


**FAILURE_MOSAIC_INVALID_CREATION_FEE**

Validation failed because the specified creation fee is invalid.


**FAILURE_TOO_MANY_MOSAIC_TRANSFERS**

Validation failed because a transfer transaction had too many attached mosaic transfers.
