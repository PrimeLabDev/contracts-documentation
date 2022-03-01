Note: For contracts APIs please check [nearapps-contracts](https://github.com/nearcomponents/nearapps-contracts/tree/development) (`development` branch).

# file-encryption

## File Escrow

### Request Share

###### Parameters

### Accept Share

###### Parameters

## File Gateway

### Encrypt Request

#### Parameters

```json
{
  "file": "very long encrypted file as string",
  "signed": {
    "signature": "26gFr4xth7W9K7HPWAxq3BLsua8oTy378mC1MYFiEXHBBpeBjP8WmJEJo8XTBowetvqbRshcQEtBUdwQcAqDyP8T",
    "publicKey": "ed25519:3LNrJmhPYHNMqDWErMpBTUVohh6CfADDr7VG8mSH3baz"
  }
}
```

#### Response

```json
{
  "file": "encrypted very long encrypted file as string"
}
```

### Decrypt Request

#### Parameters

```json
{
  "file": "encrypted very long encrypted file as string",
  "signed": {
    "signature": "26gFr4xth7W9K7HPWAxq3BLsua8oTy378mC1MYFiEXHBBpeBjP8WmJEJo8XTBowetvqbRshcQEtBUdwQcAqDyP8T",
    "publicKey": "ed25519:3LNrJmhPYHNMqDWErMpBTUVohh6CfADDr7VG8mSH3baz"
  }
}
```

#### Response

```json
{
  "file": "very long encrypted file as string"
}
```

## Access Contract

### Interface

#### Owner Management

##### Get Owner

method: `get_owner`  
description: Get the contract's owner.

###### Parameters

Has no parameters.

###### Returns

- `account_id`: string - The owner's account_id.

#### Storage Management

##### Add Storage Manager

method: `add_storage`  
description: Add a new file storage manager, such as Google Drive.

###### Parameters

- `name_hash`: string - Unique name that represents that file storage manager. Eg. "Google Drive" (should be hashed, can
  be salted).

###### Returns

Has no returns.

###### Events

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "new_storage",
    "data": [
      {
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c"
      }
    ]
  }
}
```

##### Remove Storage Manager

method: `remove_storage`  
description: Remove a file storage manager, such as Google Drive.

###### Parameters

- `name_hash`: string - Unique name that represents that file storage manager. Eg. "Google Drive" (should be hashed, can
  be salted).

###### Returns

- `removed`: boolean - whether the removed storage manager was just removed.

###### Events

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "removed_storage",
    "data": [
      {
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c"
      }
    ]
  }
}
```

##### Get Storage Managers

method: `get_storages`  
description: Get a list of registered storage managers.

###### Parameters

- `from_index`: optional string - the number of how many storage managers to skip.
- `limit`: optional number - 16-bits number to limit how many storage manager to show.

###### Returns

- `storages`: `string[]` - list of file storage managers' name_hash.

#### File Management

##### Add File

method: `add_file`  
description: Adds a new file, which is related to some storage, to be owned by some user.

###### Parameters

- `user`: string - The account_id of the user that shall own the file.
- `storage_manager`: string - The name hash of the storage manager.
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall own.
- `uri`: string - The URI or reference hash for the file location within the `storage_manager`.

###### Returns

- `added`: bool - whether the file was successfully added.

###### Events

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "file_created",
    "data": [
      {
        "owner_id": "my-account.near",
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad",
        "uri": "bfd426d349a68b483b2cc1f4d397a9deb68f5efb681b37d88777a5a707878d2d"
      }
    ]
  }
}
```

##### Remove File

method: `remove_file`  
description: Removes a file, which is related to some storage, from some user.

###### Parameters

- `user`: string - The account_id of the user that shall lose ownership of the file.
- `storage_manager`: string - name of the storage manager.
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall lose ownership.
- `uri`: string - The URI or reference hash for the file location within the `storage_manager`.

###### Returns

- `removed`: bool - whether the file was successfully removed.

###### Events

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "file_removed",
    "data": [
      {
        "owner_id": "my-account.near",
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad",
        "uri": "bfd426d349a68b483b2cc1f4d397a9deb68f5efb681b37d88777a5a707878d2d"
      }
    ]
  }
}
```

#### Access Management

##### Grant Access

method: `grant_access`  
description: Grants access to a file hash.

###### Parameters

- `user`: string - The account_id of the user that shall get authorized to access the file.
- `storage_manager`: string - name of the storage manager.
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall have access into.
- `uri`: string - The URI or reference hash for the file location within the `storage_manager`.

###### Returns

Has no returns.

###### Events

Access Created:

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "access_created",
    "data": [
      {
        "owner_id": "my-account.near",
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad",
        "uri": "bfd426d349a68b483b2cc1f4d397a9deb68f5efb681b37d88777a5a707878d2d"
      }
    ]
  }
}
```

##### Revoke Access

method: `revoke_access`  
description: Revokes access to a file hash.

###### Parameters

- `user`: string - The account_id of the user that shall be not authorized to access the file.
- `storage_manager`: string - name of the storage manager.
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall lose it's access
  into.
- `uri`: string - The URI or reference hash for the file location within the `storage_manager`.

###### Returns

Has no returns.

###### Events

Access Deleted:

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "access_deleted",
    "data": [
      {
        "owner_id": "my-account.near",
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad",
        "uri": "bfd426d349a68b483b2cc1f4d397a9deb68f5efb681b37d88777a5a707878d2d"
      }
    ]
  }
}
```

### Other Events

Events that are likely to exist, but that still don't have a related and defined method structure for the contracts.

Share Requested:

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "access_requested",
    "data": [
      {
        "owner_id": "my-account.near",
        "receiver_id": "my-account.near",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad",
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c"
      }
    ]
  }
}
```

Share Accepted:

```json
{
  "EVENT_JSON": {
    "standard": "access",
    "version": "1.0.0",
    "event": "access_accepted",
    "data": [
      {
        "owner_id": "my-account.near",
        "receiver_id": "my-account.near",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad",
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c"
      }
    ]
  }
}
```

# Message samples

#### Create Wallet

Message In:

```json
{
  "id": "4567",
  "operation": "execute",
  "contract": "testnet",
  "method": "create_account",
  "args": {
    "new_account_id": "my-account5046.testnet",
    "new_public_key": "ed25519:D5d84XpgHtTUHwg1hbvT3Ljy6LpeLnJhU34scBC1TNKp"
  },
  "sender": "my-account5046.testnet",
  "tags": {
    "app_id": "my nice app",
    "action_id": "1",
    "user_id": "my-account5046.testnet"
  }
}
```

Message Out:

```json
{
  "id": "4567",
  "operation": "execute_out",
  "success": true,
  "message": "contract call successful",
  "explorerUrl": "https://explorer.testnet.near.org/transactions/4ETZyEE2rHqPkNAez9PRvTYZVUKPvMUULJjGkibKHiFe",
  "args": true
}
```

#### Create NFT Series

Message In:

```json
{
  "id": "1234",
  "operation": "execute",
  "contract": "nft.naps.testnet",
  "method": "nft_series_create",
  "sender": "my-account3256.testnet",
  "args": {
    "name": "Title of my NFT",
    "capacity": "20",
    "creator": "vvs111.testnet"
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": "2",
    "user_id": "my-account3256.testnet"
  }
}
```

Message Out:

```json
{
  "id": "1234",
  "operation": "execute_out",
  "success": true,
  "message": "contract call successful",
  "explorerUrl": "https://explorer.testnet.near.org/transactions/CEPvP3Z4q9HJkssqrqKwRNG5djF6iFSQGBYy18yAwU5k",
  "args": "37"
}
```

#### Transfer NFT

Message In:

```json
{
  "id": "7890",
  "operation": "execute",
  "contract": "nft.naps.testnet",
  "method": "nft_series_mint",
  "sender": "my-account8246.testnet",
  "deposit": "0.01",
  "args": {
    "series_id": "37",
    "token_owner_id": "my-account.testnet",
    "token_metadata": {
      "title": null,
      "description": null,
      "media": "https://ipfs.io/ipfs/bafybeicvjdjdxhu6oglore3dw26pclogws2adk7gtmsllje6siinqq4uzy",
      "media_hash": null,
      "copies": null,
      "issued_at": null,
      "expires_at": null,
      "starts_at": null,
      "updated_at": null,
      "extra": null,
      "reference": "https://ipfs.io/ipfs/bafybeigo6bjoq6t5dl4fqgvwosplvbkbu5ri6wo3cmkxmypi4sj2j2ae54",
      "reference_hash": null
    }
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": "3",
    "user_id": "my-account8246.testnet"
  }
}
```

Message Out:

```json
{
  "id": "7890",
  "operation": "execute_out",
  "success": true,
  "message": "contract call successful",
  "explorerUrl": "https://explorer.testnet.near.org/transactions/DbUUD55qcD1ypBKCjTYSMV2LaSznxdrfABqx6Yg9xq7m",
  "args": {
    "token_id": "Title of my NFT:37:0",
    "owner_id": "my-account.testnet",
    "metadata": {
      "title": null,
      "description": null,
      "media": "https://ipfs.io/ipfs/bafybeicvjdjdxhu6oglore3dw26pclogws2adk7gtmsllje6siinqq4uzy",
      "media_hash": null,
      "copies": null,
      "issued_at": null,
      "expires_at": null,
      "starts_at": null,
      "updated_at": null,
      "extra": null,
      "reference": "https://ipfs.io/ipfs/bafybeigo6bjoq6t5dl4fqgvwosplvbkbu5ri6wo3cmkxmypi4sj2j2ae54",
      "reference_hash": null
    },
    "approved_account_ids": {}
  }
}
```

#### Send Near Tokens

description: The executor will transfer 1 NEAR from user _my-account.testnet_ into the user _my-friend.testnet._

Message In:

```json
{
  "id": "987654",
  "operation": "execute",
  "contract": "send-near.naps.testnet",
  "method": "send_logged",
  "args": {
    "sender_id": "my-account.testnet",
    "receiver_id": "my-friend.testnet",
    "amount": "1000000000000000000000000"
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": 2,
    "user_id": "my-account.testnet"
  }
}
```

Message Out:

```json
{
  "id": "987654",
  "operation": "execute_out",
  "success": true,
  "app_id": "my nice app",
  "explorerUrl": "https://explorer.near.org/wwww",
  "args": {
    "got_sent": true
  }
}
```

#### Send Nft Tokens

description: The executor will ask the SendNft to transfer _some-token-123_ token from user _my-account.testnet_ into
the user _my-friend.testnet,_ for _the.nft.testnet_ nft contract.

Message In:

```json
{
  "id": "987654",
  "operation": "execute",
  "contract": "send-nft.naps.testnet",
  "method": "send_logged",
  "args": {
    "nft_contract": "the.nft.testnet",
    "token_id": "some-token-123",
    "sender_id": "my-account.testnet",
    "receiver_id": "my-friend.testnet"
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": 2,
    "user_id": "my-account.testnet"
  }
}
```

Message Out:

```json
{
  "id": "987654",
  "operation": "execute_out",
  "success": true,
  "app_id": "my nice app",
  "explorerUrl": "https://explorer.near.org/wwww",
  "args": {
    "got_sent": true
  }
}
```

#### Create File

Message In:

```json
{
  "id": "987654",
  "operation": "execute",
  "contract": "access.naps.testnet",
  "method": "create_file",
  "args": {
    "fileHash": "jadajksdhajsd",
    "sender_id": "my-account.testnet"
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": 2,
    "user_id": "my-account.testnet"
  }
}
```

Message Out:

```json
{
  "id": "987654",
  "operation": "execute_out",
  "success": true,
  "app_id": "my nice app",
  "explorerUrl": "https://explorer.near.org/wwww",
  "args": true
}
```

#### Delete File

Message In:

```json
{
  "id": "987654",
  "operation": "execute",
  "contract": "access.naps.testnet",
  "method": "delete_file",
  "args": {
    "fileHash": "jadajksdhajsd",
    "sender_id": "my-account.testnet"
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": 2,
    "user_id": "my-account.testnet"
  }
}
```

Message Out:

```json
{
  "id": "987654",
  "operation": "execute_out",
  "success": true,
  "app_id": "my nice app",
  "explorerUrl": "https://explorer.near.org/wwww",
  "args": true
}
```

#### Grant File Access

Message In:

```json
{
  "id": "987654",
  "operation": "execute",
  "contract": "access.naps.testnet",
  "method": "grant_access",
  "args": {
    "fileHash": "jadajksdhajsd",
    "sender_id": "my-account.testnet",
    "receiver_id": "my-friend.testnet"
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": 2,
    "user_id": "my-account.testnet"
  }
}
```

Message Out:

```json
{
  "id": "987654",
  "operation": "execute_out",
  "success": true,
  "app_id": "my nice app",
  "explorerUrl": "https://explorer.near.org/wwww",
  "args": true
}
```

#### Revoke File Access

Message In:

```json
{
  "id": "987654",
  "operation": "execute",
  "contract": "access.naps.testnet",
  "method": "revoke_access",
  "args": {
    "fileHash": "jadajksdhajsd",
    "receiver_id": "my-friend.testnet"
  },
  "tags": {
    "app_id": "my nice app",
    "action_id": 2,
    "user_id": "my-account.testnet"
  }
}
```

Message Out:

```json
{
  "id": "987654",
  "operation": "execute_out",
  "success": true,
  "app_id": "my nice app",
  "explorerUrl": "https://explorer.near.org/wwww",
  "args": true
}
```
