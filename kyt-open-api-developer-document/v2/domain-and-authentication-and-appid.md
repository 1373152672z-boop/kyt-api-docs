# Domain & Authentication & APPID

## Domain & Authentication & APPID

### 1. API Domain

```
https://openapi.trustformer.info
```

All V3 API endpoints are prefixed with this domain.

***

### 2. Authentication Mechanism

KYT will provide each client with:

* `apikey`
* `secret`

When calling any API:

* `apikey` must be passed as a request parameter.
* `timestamp` and `sign` must be included in the request header.

***

### 3. Signature Algorithm

The signature is calculated using the following rule:

```
sha256("timestamp={timestamp}&secret={secret}")
```

#### Example

Before encryption:

```
timestamp=1677148682&secret=9e3df800bbcbb1b8fc97bf78ed95a95a92aa3a155d270f1e48eb330c2d435321
```

After SHA256 encryption:

```
110a20dcbe1fef5456051a8887c8d1aeba637bbc624e606697fb82a7e7ded604
```

You may use any SHA256 tool or library to generate the signature.

***

### 4. Request Header Parameters

| Parameter | Type   | Required | Description              |
| --------- | ------ | -------- | ------------------------ |
| timestamp | int    | Yes      | Unix timestamp (seconds) |
| sign      | string | Yes      | SHA256 signature         |

***

### 5. APP\_ID Usage

`app_id` is used to distinguish different business applications under the same client.

It must be passed as a required parameter in all V3 business APIs.

Each `app_id`:

* Corresponds to a specific application
* Has independent risk strategy configuration
* Has independent risk monitoring records

***

### 6. Authentication Failure Response

If the API key is invalid or expired, the interface returns:

```
{
  "code": -1,
  "data": {},
  "message": "api_key is invalid"
}
```

***

### 7. Notes

* The timestamp must be the current server time (in seconds).
* It is recommended to keep the time difference within ±5 minutes.
* Requests with invalid signatures will be rejected.
* Keep your `secret` strictly confidential.
