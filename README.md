# file-encryption

## File Escrow

### Request Share

###### Parameters

### Accept Share

###### Parameters

## File Gateway

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
- `name_hash`: string - Unique name that represents that file storage manager. Eg. "Google Drive" (should be hashed, can be salted).

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
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
      }
    ]
  }
}
```

##### Remove Storage Manager
method: `remove_storage`  
description: Remove a file storage manager, such as Google Drive.

###### Parameters
- `name_hash`: string - Unique name that represents that file storage manager. Eg. "Google Drive" (should be hashed, can be salted).

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
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
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
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall lose it's access into.
- `uri`: string - The URI or reference hash for the file location within the `storage_manager`.

###### Returns
Has no returns.

###### Events
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
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
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
        "storage_manager": "3c747963faee04a635854300c3c4bdf69273078d345429d48db5d6d9db92fb3c",
      }
    ]
  }
}
```
