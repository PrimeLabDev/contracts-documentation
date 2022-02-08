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
- `name`: string - Unique name that represents that file storage manager. Eg. "Google Drive".

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
        "storage_manager": "Google Drive",
      }
    ]
  }
}
```

##### Remove Storage Manager
method: `remove_storage`  
description: Remove a file storage manager, such as Google Drive.

###### Parameters
- `name`: string - Unique name that represents that file storage manager. Eg. "Google Drive".

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
        "storage_manager": "Google Drive",
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
- `storages`: `string[]` - list of file storage managers' names.

#### File Management

##### Add File
method: `add_file`  
description: Adds a new file, which is related to some storage, to be owned by some user.

###### Parameters
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall own.
- `storage_manager`: string - name of the storage manager.
- `user`: string - The account_id of the user that shall own the file.

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
        "storage_manager": "Google Drive",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
      }
    ]
  }
}
```

##### Remove File
method: `remove_file`  
description: Removes a file, which is related to some storage, from some user.

###### Parameters
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall lose ownership.
- `storage_manager`: string - name of the storage manager.
- `user`: string - The account_id of the user that shall lose ownership of the file.

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
        "storage_manager": "Google Drive",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
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
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall have access into.
- `storage_manager`: string - name of the storage manager.
- `user`: string - The account_id of the user that shall get authorized to access the file.

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
        "storage_manager": "Google Drive",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
      }
    ]
  }
}
```

##### Revoke Access
method: `revoke_access`  
description: Revokes access to a file hash.

###### Parameters
- `filehash`: string - The hexadecimal representation of the hash/id of the file that the `user` shall lose it's access into.
- `storage_manager`: string - name of the storage manager.
- `user`: string - The account_id of the user that shall be not authorized to access the file.

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
        "storage_manager": "Google Drive",
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
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
        "storage_manager": "Google Drive",
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
        "storage_manager": "Google Drive",
      }
    ]
  }
}
```
