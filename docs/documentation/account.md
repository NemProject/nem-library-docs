# Account related requests

This chapter will guide you through the process of retrieving account information from a NEM Infrastructure Server (NIS). The information that can be retrieved is the durable account data, its meta data and information about transactions and harvested blocks.

NIS supports two different kind of accounts: normal accounts and multsig (short for: multi signature) accounts:

**Normal accounts:**

Normal accounts are created and controlled by a private key. Any action for the account like sending NEM to another account via a transfer transaction is signed with this private key. If an attacker gains knowledge of the private key, he/she can rob the account. The private key must therefore be kept secret by all means.

**Multisig accounts:**

Multisig accounts can be created by converting a normal account to a multisig account via a aggregate modification transaction. This adds cosignatories to the account. After that modification, only the cosignatories can initiate an action for the account. Any action must be signed by all cosignatories. This makes a multisig account significantly more secure than a normal account. When a single cosignatory private key is gained by an attacker, the attacker still can`t initiate any action on the account since all cosignatories must sign. It is strongly recommended to convert any account holding a significantly high amount of NEM into a multisig account with at least 3 cosignatories. Once converted to a multisig account, the original private key for the account plays no role any more.

[Official Source](https://bob.nem.ninja/docs/#account-related-requests)

## Keypair concept

NEM Library replaces the Keypair model, which usually holds the public and private key, with the [Account](#account) model. The reason is that we aim to keep the private key as secret as possible, just providing a set of methods where the private key is involved.

# AccountHttp definition

```typescript
export declare class AccountHttp extends HttpEndpoint {
    constructor(nodes?: ServerConfig[]);
    /**
     * Gets an AccountInfoWithMetaData for an account.
     * @param address - Address
     * @return Observable<AccountInfoWithMetaData>
     */
    getFromAddress(address: Address): Observable<AccountInfoWithMetaData>;
    /**
     * Gets an AccountInfoWithMetaData for an account with publicKey
     * @param publicKey - NEM
     * @return Observable<AccountInfoWithMetaData>
     */
    getFromPublicKey(publicKey: string): Observable<AccountInfoWithMetaData>;
    /**
     * Given a delegate (formerly known as remote) account's address, gets the AccountMetaDataPair for the account for which the given account is the delegate account.
     * If the given account address is not a delegate account for any account, the request returns the AccountMetaDataPair for the given address.
     * @param address - Address
     * @return Observable<AccountInfoWithMetaData>
     */
    getOriginalAccountDataFromDelegatedAccountAddress(address: Address): Observable<AccountInfoWithMetaData>;
    /**
     * retrieve the original account data by providing the public key of the delegate account.
     * @param publicKey - string
     * @return Observable<AccountInfoWithMetaData>
     */
    getOriginalAccountDataFromDelegatedAccountPublicKey(publicKey: string): Observable<AccountInfoWithMetaData>;
    /**
     * Gets the AccountMetaData from an account.
     * @param address - NEM Address
     * @return Observable<AccountStatus>
     */
    status(address: Address): Observable<AccountStatus>;
    /**
     * A transaction is said to be incoming with respect to an account if the account is the recipient of the transaction.
     * In the same way outgoing transaction are the transactions where the account is the sender of the transaction.
     * Unconfirmed transactions are those transactions that have not yet been included in a block.
     * Unconfirmed transactions are not guaranteed to be included in any block
     * @param address - The address of the account.
     * @param params
     */
    incomingTransactions(address: Address, params?: QueryParams): Observable<Transaction[]>;
    /**
     * Paginaged version of incomingTransactions request
     * @param address
     * @param params
     */
    incomingTransactionsPaginated(address: Address, params?: QueryParams): Pageable<Transaction[]>;
    /**
     * Gets an array of transaction meta data pairs where the recipient has the address given as parameter to the request.
     * A maximum of 25 transaction meta data pairs is returned. For details about sorting and discussion of the second parameter see Incoming transactions.
     * @param address - The address of the account.
     * @param params
     */
    outgoingTransactions(address: Address, params?: QueryParams): Observable<Transaction[]>;
    /**
     * Paginaged version of outgoingTransactions request
     * @param address
     * @param params
     * @param params
     */
    outgoingTransactionsPaginated(address: Address, params?: QueryParams): Pageable<Transaction[]>;
    /**
     * Gets an array of transaction meta data pairs for which an account is the sender or receiver.
     * A maximum of 25 transaction meta data pairs is returned.
     * For details about sorting and discussion of the second parameter see Incoming transactions.
     * @param address - The address of the account.
     * @param params
     */
    allTransactions(address: Address, params?: QueryParams): Observable<Transaction[]>;
    /**
     * Paginaged version of allTransactions request
     * @param address
     * @param params
     */
    allTransactionsPaginated(address: Address, params?: QueryParams): Pageable<Transaction[]>;
    /**
     * Gets the array of transactions for which an account is the sender or receiver and which have not yet been included in a block
     * @param address - NEM Address
     * @return Observable<Transaction[]>
     */
    unconfirmedTransactions(address: Address): Observable<Transaction[]>;
    /**
     * Gets an array of harvest info objects for an account.
     * @param address - Address
     * @param id - string (optional)
     * @return Observable<AccountHarvestInfo[]>
     */
    getHarvestInfoDataForAnAccount(address: Address, id?: string): Observable<AccountHarvestInfo[]>;
    /**
     * Paginaged version of allTransactions request
     * @param address
     * @param id
     * @returns {HarvestInfoPageable}
     */
    getHarvestInfoDataForAnAccountPaginated(address: Address, id?: string): Pageable<AccountHarvestInfo[]>;
    /**
     * Gets an array of account importance view model objects.
     * @return Observable<AccountImportanceInfo[]>
     */
    getAccountImportances(): Observable<AccountImportanceInfo[]>;
    /**
     * Gets an array of namespace objects for a given account address.
     * The parent parameter is optional. If supplied, only sub-namespaces of the parent namespace are returned.
     * @param address - Address
     * @param parent - The optional parent namespace id.
     * @param id - The optional namespace database id up to which namespaces are returned.
     * @param pageSize - The (optional) number of namespaces to be returned.
     * @return Observable<Namespace[]>
     */
    getNamespaceOwnedByAddress(address: Address, parent?: string, pageSize?: number, id?: string): Observable<Namespace[]>;
    /**
     * Gets an array of mosaic definition objects for a given account address. The parent parameter is optional.
     * If supplied, only mosaic definitions for the given parent namespace are returned.
     * The id parameter is optional and allows retrieving mosaic definitions in batches of 25 mosaic definitions.
     * @param address - The address of the account.
     * @param parent - The optional parent namespace id.
     * @param id - The optional mosaic definition database id up to which mosaic definitions are returned.
     * @return Observable<MosaicDefinition[]>
     */
    getMosaicCreatedByAddress(address: Address, parent?: string, id?: string): Observable<MosaicDefinition[]>;
    /**
     * Gets an array of mosaic objects for a given account address.
     * @param address - Address
     * @return Observable<Mosaic[]>
     */
    getMosaicOwnedByAddress(address: Address): Observable<Mosaic[]>;
    /**
     * Unlocks an account (starts harvesting).
     * @param host - string
     * @param privateKey - string
     * @return Observable<boolean>
     */
    unlockHarvesting(host: string, privateKey: string): Observable<boolean>;
    /**
     * Locks an account (stops harvesting).
     * @param host - string
     * @param privateKey - string
     * @return Observable<boolean>
     */
    lockHarvesting(host: string, privateKey: string): Observable<boolean>;
    /**
     * Each node can allow users to harvest with their delegated key on that node.
     * The NIS configuration has entries for configuring the maximum number of allowed harvesters and optionally allow harvesting only for certain account addresses.
     * The unlock info gives information about the maximum number of allowed harvesters and how many harvesters are already using the node.
     * @return Observable<NodeHarvestInfo>
     */
    unlockInfo(): Observable<NodeHarvestInfo>;
    /**
     * Gets historical information for an account.
     * @param address - The address of the account.
     * @param startHeight - The block height from which on the data should be supplied.
     * @param endHeight - The block height up to which the data should be supplied. The end height must be greater than or equal to the start height.
     * @param increment - The value by which the height is incremented between each data point. The value must be greater than 0. NIS can supply up to 1000 data points with one request. Requesting more than 1000 data points results in an error.
     * @return Observable<AccountHistoricalInfo[]>
     */
    getHistoricalAccountData(address: Address, startHeight: number, endHeight: number, increment: number): Observable<AccountHistoricalInfo[]>;
    /**
     * Gets historical information for an array of accounts.
     * @param addresses - The addresses of the accounts as an array of addresses.
     * @param startHeight - The block height from which on the data should be supplied.
     * @param endHeight - The block height up to which the data should be supplied. The end height must be greater than or equal to the start height.
     * @param increment - The value by which the height is incremented between each data point. The value must be greater than 0. NIS can supply up to 1000 data points with one request. Requesting more than 1000 data points results in an error.
     * @return Observable<AccountHistoricalInfo[][]>
     */
    getBatchHistoricalAccountData(addresses: Address[], startHeight: number, endHeight: number, increment: number): Observable<AccountHistoricalInfo[][]>
    /**
     * Gets batch information for an array of accounts.
     * @param addresses - The addresses of the accounts as an array.
     * @return Observable<AccountInfoWithMetadata[]>
     */
    getBatchAccountData(addresses: Address[]): Observable<AccountInfoWithMetaData[]>
}

```

### QueryParams

```typescript
export interface QueryParams {
    /**
     * (Optional) The xem of transactions returned. Between 5 and 100, otherwise 10
     */
    pageSize?: number;
    /**
     * (Optional) The 256 bit sha3 hash of the transaction up to which transactions are returned.
     */
    hash?: string;
    /**
     * (Optional) The transaction id up to which transactions are returned. This parameter will prevail over hash.
     */
    id?: string;
}
```

# AccountHttp usage

```typescript
import {AccountHttp, NEMLibrary, NetworkTypes, Address} from "nem-library";

// Initialize NEMLibrary for TEST_NET Network
NEMLibrary.bootstrap(NetworkTypes.TEST_NET);

const address = new Address("");

const accountHttp = new AccountHttp();
accountHttp.getFromAddress(address).subscribe(accountInfoWithMetaData => {
    console.log(accountInfoWithMetaData);
});
```


Output:

```
AccountInfoWithMetaData {
  balance: 
   Balance {
     balance: 50481110745315,
     vestedBalance: 50480744575985,
     unvestedBalance: 366169330 },
  importance: 0.005735794657626706,
  publicAccount: 
   PublicAccount {
     address: 
      Address {
        value: 'TALICEROONSJCPHC63F52V6FY3SDMSVAEUGHMB7C',
        networkType: 152 },
     publicKey: '74375c15c6ce6bdbde59be88a069745a0de34444ea933f8c9f46ef407cf30196' },
  harvestedBlocks: 116319,
  cosignatoriesCount: undefined,
  minCosignatories: undefined,
  status: 'UNLOCKED',
  remoteStatus: 'INACTIVE',
  cosignatoryOf: [],
  cosignatories: [] }
```

[Run the code](https://github.com/aleixmorgadas/nem-library-examples/blob/master/concepts/account/AccountHttpExample.ts)

# Models

## <a name="account"></a> Account

```typescript
/**
 * Account model
 */
export declare class Account extends PublicAccount {
    
    private readonly privateKey;
    /**
     * Sign a transaction
     * @param transaction
     * @returns {{data: any, signature: string}}
     */
    signTransaction(transaction: Transaction): SignedTransaction;
    
    /**
     * constructor with private key
     * @param privateKey
     * @returns {Account}
     */
    static createWithPrivateKey(privateKey: string): Account;
    
    /**
     * Create a new encrypted Message
     * @param message
     * @param recipientPublicAccount
     * @returns {EncryptedMessage}
     */
    encryptMessage(message: string, recipientPublicAccount: PublicAccount): EncryptedMessage;
    
    /**
     * Decrypts an encrypted message
     * @param encryptedMessage
     * @param recipientPublicAccount
     * @returns {PlainMessage}
     */
    decryptMessage(encryptedMessage: EncryptedMessage, recipientPublicAccount: PublicAccount): PlainMessage;
}
```


## PublicAccount

```typescript

/**
 * Public account
 */
export declare class PublicAccount {
    
    readonly address: Address;
    readonly publicKey: string;
    
    /**
     * @returns {boolean}
     */
    hasPublicKey(): boolean;
    
    /**
     * Creates a new PublicAccount from a public key
     * @param publicKey
     * @returns {PublicAccount}
     */
    static createWithPublicKey(publicKey: string): PublicAccount;
}
```

## Address

```typescript
/**
 * Address model
 */
export declare class Address {
    
    private readonly value;
    private readonly networkType;
    constructor(address: string);
    
    /**
     * Get address in plain format ex: TALICEROONSJCPHC63F52V6FY3SDMSVAEUGHMB7C
     * @returns {string}
     */
    plain(): string;
    
    /**
     * Get address in pretty format ex: TALICE-ROONSJ-CPHC63-F52V6F-Y3SDMS-VAEUGH-MB7C
     * @returns {string}
     */
    pretty(): string;
    
    /**
     * Address network
     * @returns {number}
     */
    network(): NetworkTypes;
}

```

## Balance

```typescript
/**
 * Balance model
 */
export declare class Balance {
    
    /**
     * The balance of the account in micro NEM.
     */
    readonly balance: number;
    
    /**
     * The vested part of the balance of the account in micro NEM.
     */
    readonly vestedBalance: number;
    
    /**
     * The unvested part of the balance of the account in micro NEM.
     */
    readonly unvestedBalance: number;
}

```
## AccountInfo

```typescript
export declare enum RemoteStatus {
    REMOTE = "REMOTE",
    ACTIVATING = "ACTIVATING",
    ACTIVE = "ACTIVE",
    DEACTIVATING = "DEACTIVATING",
    INACTIVE = "INACTIVE",
}
export declare enum Status {
    UNKNOWN = "UNKNOWN",
    LOCKED = "LOCKED",
    UNLOCKED = "UNLOCKED",
}

/**
 * The account structure describes basic information for an account.
 */
export declare class AccountInfo {
    
    /**
     * The balance of the account in micro NEM.
     */
    readonly balance: Balance;
    
    /**
     * The importance of the account.
     */
    readonly importance: number;
    
    /**
     * The public key of the account.
     */
    readonly publicAccount: PublicAccount;
    
    /**
     * The number blocks that the account already harvested.
     */
    readonly harvestedBlocks: number;
    
    /**
     * Total number of cosignatories
     */
    readonly cosignatoriesCount?: number;
    
    /**
     * Minimum number of cosignatories needed for a transaction to be processed
     */
    readonly minCosignatories?: number;
}

export declare class AccountInfoWithMetaData extends AccountInfo {
    
    /**
     * The harvesting status of a queried account
     */
    readonly status: Status;
    
    /**
     * The status of remote harvesting of a queried account
     */
    readonly remoteStatus: RemoteStatus;
    
    /**
     * JSON array of AccountInfo structures. The account is cosignatory for each of the accounts in the array.
     */
    readonly cosignatoryOf: AccountInfo[];
    
    /**
     * JSON array of AccountInfo structures. The array holds all accounts that are a cosignatory for this account.
     */
    readonly cosignatories: AccountInfo[];
}

export declare class AccountStatus {
    
    /**
     * The harvesting status of a queried account
     */
    readonly status: Status;
    
    /**
     * The status of remote harvesting of a queried account
     */
    readonly remoteStatus: RemoteStatus;
    
    /**
     * JSON array of AccountInfo structures. The account is cosignatory for each of the accounts in the array.
     */
    readonly cosignatoryOf: AccountInfo[];
    
    /**
     * JSON array of AccountInfo structures. The array holds all accounts that are a cosignatory for this account.
     */
    readonly cosignatories: AccountInfo[];
}

```
## AccountHarvestInfo

```typescript
/**
 * A HarvestInfo object contains information about a block that an account harvested.
 */
export declare class AccountHarvestInfo {
    
    /**
     * The number of seconds elapsed since the creation of the nemesis block.
     */
    readonly timeStamp: number;
    
    /**
     * The database id for the harvested block.
     */
    readonly id: number;
    
    /**
     * The block difficulty. The initial difficulty was set to 100000000000000. The block difficulty is always between one tenth and ten times the initial difficulty.
     */
    readonly difficulty: number;
    
    /**
     * The total fee collected by harvesting the block.
     */
    readonly totalFee: number;
    
    /**
     * The height of the harvested block.
     */
    readonly height: number;
}

```

## AccountHistoricalInfo

```typescript
/**
 * Nodes can support a feature for retrieving historical data of accounts.
 * If this is supported, it returns an array of AccountHistoricalInfo
 */
export declare class AccountHistoricalInfo {
    
    /**
     * The balance of the account in micro NEM.
     */
    readonly balance: Balance;
    
    /**
     * The importance of the account.
     */
    readonly importance: number;
    
    /**
     * The public key of the account.
     */
    readonly address: Address;
    
    /**
     * The page rank part of the importance.
     */
    readonly pageRank: number;
}
```

## AccountImportanceInfo

```typescript
/**
 * Each account is assigned an importance in the NEM network. The ability of an account to generate new blocks is proportional to its importance. The importance is a number between 0 and 1.
 */
export declare class AccountImportanceInfo {
    
    /**
     * The address of the account.
     */
    readonly address: Address;
    
    /**
     * Substructure that describes the importance of the account.
     */
    readonly importance: AccountImportanceData;
}

/**
 * Substructure that describes the importance of the account.
 */
export declare class AccountImportanceData {
    /**
     * Indicates if the fields "score", "ev" and "height" are available.isSet can have the values 0 or 1. In case isSet is 0 the fields are not available.
     */
    readonly isSet: number;
    
    /**
     * The importance of the account. The importance ranges between 0 and 1.
     */
    readonly score?: number;
    
    /**
     * The page rank portion of the importance. The page rank ranges between 0 and 1.
     */
    readonly ev?: number;
    
    /**
     * The height at which the importance calculation was performed.
     */
    readonly height?: number;
}

```
## NodeHarvestInfo

```typescript
export declare class NodeHarvestInfo {
    
    /**
     * Maximum unlocked slots
     */
    readonly maxUnlocked: number;
    
    /**
     * Number of slots unlocked
     */
    readonly numUnlocked: number;
}

```

## Pageable

```typescript
/**
 * Pageable class
 */
export declare class Pageable<T> extends Subject<T> {
    /**
     * Execute next page
     */
    nextPage(): void;
}
```
