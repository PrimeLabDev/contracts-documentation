# file-encryption

## File Escrow

### Request Share

#### Parameters

### Accept Share

#### Parameters

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

##### Grant Access

method: `grant_access`  
description: Grants access to a file hash.

###### Parameters

- `user`: string - The account_id of the user that will have a NFT contract disabled for them.

###### Returns

- `account_id`: string - The owner's account_id.

### Events

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
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
      }
    ]
  }
}
```

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
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
      }
    ]
  }
}
```

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
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
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
        "file_hash": "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"
      }
    ]
  }
}
```