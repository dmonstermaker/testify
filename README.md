
### Schema
```sql
-- user_identities

| id                       | type | uid | is_verified | last_verified       | last_verified_source |
|--------------------------|------|-----|-------------|---------------------|----------------------|
| abhijeet.m@stayzilla.com | EML  | 123 | 1           | 2016-11-22 09:21:31 | WEBSITE              |
| 8126688376               | MOB  | 123 | 1           | 2016-11-24 10:33:32 | APP_ANDROID          |
| 100001533612613          | FCB  | 123 | 1           | 2016-11-22 09:15:05 | MSITE                |
```

### Protobuf

```protobuf
syntax = 'proto3';

package users;
// https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto
import "google/protobuf/timestamp.proto";

message Identity {
  string id = 1;
  string type = 2;
  int32 uid = 3;
  bool is_verified = 4;
  string last_verified_source = 5;
  google.protobuf.Timestamp last_verified = 6;
  google.protobuf.Timestamp created_at = 7;
  google.protobuf.Timestamp updated_at = 8;
}
```

### Endpoints

**Get all identities of user**

**Request:**
```sh
curl -i \
    -X GET \
    -H "Content-type: application/json" \
    "https://api.stayzilla.com/v1/users/123/identities"
```

**Response:**
```json
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [
    {
      "id": "abhijeet@stayzilla.com",
      "type": "EML",
      "uid": 123,
      "is_verified": true,
      "last_verified_source": "WEBSITE",
      "last_verified_time": "2016-11-24T09:21:31Z",
      "created_at": "2016-11-24T09:21:31Z",
      "updated_at": "2016-11-24T09:21:31Z"
    },
    {
      "id": "100001533612613",
      "type": "FCB",
      "uid": 123,
      "is_verified": true,
      "last_verified_source": "MSITE",
      "last_verified_time": "2016-11-24T11:31:04Z",
      "created_at": "2016-11-24T11:31:04Z",
      "updated_at": "2016-11-24T11:31:04Z"
    },
    {
      "id": "8126688376",
      "type": "MOB",
      "uid": 123,
      "is_verified": true,
      "last_verified_source": "APP_ANDROID",
      "last_verified_time": "2016-11-24T10:33:32Z",
      "created_at": "2016-11-24T10:33:32Z",
      "updated_at": "2016-11-24T10:33:32Z"
    }
  ]
}
```

**Update an identity of user**

**Request:**
```sh
curl -i \
    -X PUT \
    -H "Content-type: application/json" \
    -d '{
        "id": "94156667777",
        "type": "MOB",
        "source": "HOST_APP_ANDROID",
        "verification_token": "053835ab7fe6368b2f1fa1603a7766e2fe316f7e"
    }' \
    "https://api.stayzilla.com/v1/users/123/identities"
```

**Response:**
```json
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": {
    "updated": true
  }
}
```

