---
title: "Authentication Method"
keywords: 'QuanXiang Cloud, API'
description: 'API authentication method description'
linkTitle: "Authentication Method"
weight: 7320
---

QuanXiang Cloud Platform currently supports signature method only. The detailed configuration description is as follows.

## signature method

Refer to the following example for the signature encryption process. The following table shows the encryption commands supported by QuanXiang Cloud Low Code Platform.

{{< alert tip >}}

**Instruction**

The signature encryption process performs character processing (encoding, sorting), encryption, digest signing, and signing with key as needed, and the encryption process must use Base64 encoding or Hex encoding methods for string conversion.

{{</ alert >}}



### Character processing

Character processing includes encoding, sorting, and supports the following commands:
{{<table >}}
| Command     | Description           | Subcommand 1 and its description                                            | Subcommand 2 and its description                                            | Subcommand 3 and its description                             |
| -------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------------------- |
| `base64` | Base64 encoding    | <li>std: STD format</li><li>url: URL format</li>                 | <li>encode: encoding </li><li>decode: Decoding</li>                   | -                                             |
| `hex`    | Hex encoding       | <li>encode: encoding </li><li>decode: decoding</li>                   | -                                                            | -                                             |
| `append` | For appending strings | <li>begin: Add at the head</li><li>end: Add at the end</li>           | <APPEND_STR>: The appended string                                   | -                                             |
| `url`    | URL encoding       | <li>path: Path encoding </li><li>query: Query encoding </li>           | -                                                            | -                                             |
| `sort`   | For parameter sorting   | <li>json: Default output JSON format</li><li>xml: Output XML format</li><li>query: Output Query format</li> | <li>same: Field names remain unchanged (default)</li><li>snake: underline split, foo_bar</li><li>gonic: hump nomenclature, fooBar</li> | <li>desc: Sorted in descending order</li><li>asc: Sorted in ascending order</li> |
{{</table >}}


### Encryption
{{<table >}}
| Command  | Description         | Subcommand 1 and its description                          | Subcommand 2 and its description                                            | Subcommand 3 and its description                          | Subcommand 4 and its description   |
| ----- | ------------ | ------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------ | ------------------ |
| `aes` | AES encryption/decryption | CBC: CBC Model                              | <li>pkcs5: PKCS5 Fill Method</li><li>pkcs7: PKCS7 Fill Method</li> | <li>encode: encoding</li><li>decode: decoding</li> | <SECRET_KEY>: Key |
| `rsa` | RSA encryption/decryption | <li>encode: encoding</li><li>decode: decoding</li> | <SECRET_KEYS>: key group, can have multiple segments, and finally spell out the complete key          | -                                          | -                  |
{{</table >}}


### Abstract Signature
{{<table >}}

| Command    | Description                 | Subcommand and its description                                               |
| ------- | -------------------- | ------------------------------------------------------------ |
| `md5`   | Used to calculate MD5 HASH values | [<PREFIX>]: Optional, HASH result prefix string                        |
| `crc32` | Used to calculate CRC32       | <li>[IEEE]: Optional, IEEE polynomial support</li><li>[CASTAGNOLI]: Optional, Castagnoli polynomial support</li> |
| `crc64` | Used to calculate CRC64       | <li>[ISO]: Optional, ISO polynomial support</li><li>[ECMA]: Optional, ECMA polynomial support</li> |
{{</table >}}

### Signature with key
{{<table >}}
| Command     | Description                         | Subcommand and its description               |
| -------- | ---------------------------- | ---------------------------- |
| `sha1`   | Used to calculate HMAC sha1 HASH values   | <SECRET_KEY>: Key for signing |
| `sha256` | Used to calculate HMAC sha256 HASH values | <SECRET_KEY>: Key for signing |
{{</table >}}


### Example

```
sort query gonic asc|append begin GET\n/iaas/\n|sha256 <SECRET_KEY>|base64 std encode
```

Signature method processing steps as shown above:

1. Use hump naming to sort the parameters in ascending order and output them in query format. For example:

   ```
   action.1=foo&action.2=bar&age=18&name=bob
   ```

2. Append the string GET\n/iaas/\n at the head. For example.

   ```
   GET\n/iaas/\naction.1=foo&action.2=bar&age=18&name=bob
   ```

3. Use <SECRET_KEY> to perform HMAC sha256 calculation with the above string.

4. The above hash values are base64 std encoded to generate the final Signature string for server validation.























