# Collections

## lists
- users
- verification
- scratchpad
- sfa_token
- mfu_profiles
- mfu_requests
- mfu_nct

## users

users collection stores user profile details like user id, user credential, audi, traits etc.

### example

```json
 {
  "_id": "ZVX1Z12L",
  "audit": {
    "createdAt": "2023-11-09T06:47:57.634Z",
    "lastUpdatedAt": "2023-11-09T06:47:57.634Z"
  },
  "credentials": {
    "mpin": {
      "method": "bcrypt",
      "value": "$2a$10$sqJLF2wG48NuD228YDXKseLRvpziPFXNsQsoMkAFXKdaqm9HADCVG"
    },
    "password": {
      "method": "bcrypt",
      "value": "$2a$10$Kwgj.LKGzXl7hIa8nYK/2.6SOK3u3uAfAFYnNr1UET1XXOLjc/kA6"
    }
  },
  "lastEvent": {
    "createDate": "2023-12-05T09:58:12.645Z",
    "eventType": "USER_LOGIN_FAILURE",
    "payload": "{\"userId\":\"ZVX1Z12L\",\"emailId\":\"test1@gmail.com\",\"userAgent\":null,\"deviceId\":\"goldfish_x86_64\",\"ipAddress\":null,\"os\":null}",
    "routingKey": "user.login-failure"
  },
  "realm": "internal",
  "schemaVer": 0,
  "traits": {
    "general": {
      "email": "test1@gmail.com",
      "emailVerified": true,
      "firstName": "T",
      "lastName": "D",
      "phoneNumber": "7755221144",
      "phoneVerified": true
    }
  },
  "userType": "customer"
}
```

### visual

```puml
@startjson
{
  "_id": "ZVX1Z12L",
  "audit": {
    "createdAt": "2023-11-09T06:47:57.634Z",
    "lastUpdatedAt": "2023-11-09T06:47:57.634Z"
  },
  "credentials": {
    "mpin": {
      "method": "bcrypt",
      "value": "$2a$10$sqJLF2wG48NuD228YDXKseLRvpziPFXNsQsoMkAFXKdaqm9HADCVG"
    },
    "password": {
      "method": "bcrypt",
      "value": "$2a$10$Kwgj.LKGzXl7hIa8nYK/2.6SOK3u3uAfAFYnNr1UET1XXOLjc/kA6"
    }
  },
  "lastEvent": {
    "createDate": "2023-12-05T09:58:12.645Z",
    "eventType": "USER_LOGIN_FAILURE",
    "payload": "{\"userId\":\"ZVX1Z12L\",\"emailId\":\"test1@gmail.com\",\"userAgent\":null,\"deviceId\":\"goldfish_x86_64\",\"ipAddress\":null,\"os\":null}",
    "routingKey": "user.login-failure"
  },
  "realm": "internal",
  "schemaVer": 0,
  "traits": {
    "general": {
      "email": "test1@gmail.com",
      "emailVerified": true,
      "firstName": "T",
      "lastName": "D",
      "phoneNumber": "7755221144",
      "phoneVerified": true
    }
  },
  "userType": "customer"
}
@endjson
```

### dictionary

field | description | characteristics | is enum | example 
-----|------------|-------------------|---------|------------
_id  | the identifier of the user | ObjectID | no | QC7G-Q47E-EFWU 
audit | Audit fields | Object | no  | holding object
audit.createdAt | when was this document created | Object | no  | Object
audit.lastUpdated | when was this document last updated | Object | no | Object
credentials | credentials of users | Object | no | Object
credentials.mpin | mpin of users | Object | no | Object
credentials.mpin.method | encryption method | String | no | bcrypt
credentials.mpin.value | encrypted mpin value | String | no | $2a$10$sqJLF2wG48NuD228YDXKseLRvpziPFXNsQsoMkAFXKdaqm9HADCVG
credentials.password | stored password | Object | no | Object
credentials.password.method | encryption method | String | no | bcrypt
credentials.password.value | encrypted password value | String | no | $2a$10$Kwgj.LKGzXl7hIa8nYK/2.6SOK3u3uAfAFYnNr1UET1XXOLjc/kA6
lastEvent | when last even occur | Object | no | Object
lastEvent.createDate | when user created | Date | no | 2023-12-05T09:58:12.645Z
lastEvent.eventType | what is last event | String | no | USER_LOGIN_FAILURE
lastEvent.payload | what was the payload | String | no | "{\"userId\":\"ZVX1Z12L\",\"emailId\":\"test1@gmail.com\",\"userAgent\":null,\"deviceId\":\"goldfish_x86_64\",\"ipAddress\":null,\"os\":null}"
lastEvent.routingKey | routing key for messaging | String | no | user.login-failure
realm | realm of user | String | no | "internal"
schemaVer | schema version of collection | Int32 | no | 0
traits | user traits | Object | no | Object
traits.general | general traits | Object | no | Object
traits.general.email | email of user | String | no | test1@gmail.com
traits.general.emailVerified | if email verified | boolean | no | true
traits.general.firstName | first name of user | String | no | Haris
traits.general.lastName | last name of user | String | no | Faiz
traits.general.phoneNumber | phone number | String | no | 7755221144
traits.general.phoneVerified | if phone verified | boolean | no | true
traits.general.address | user address | Object | no | Object
traits.general.address.addressLine1 | address line 1 | String | no | Gachibowli
traits.general.address.addressLine2 | address line 2 | String | no | String
traits.general.address.city | city | String | no | Hyderabad
traits.general.address.state | state | String | no | Telangana
traits.general.address.pinCode | pin code | String | no | 500001
traits.general.address.country | country | String | no | India
traits.general.dateOfBirth | date of birth | Date | no | 2002-12-05
traits.customer | customer traits | Object | no | Object
traits.customer.pan | pan | String | no| ACMP9837D
traits.customer.membershipPlan | membership plan | String | no | GOLD
traits.customer.kyc | kyc | Object | no | Object
traits.customer.kyc.status | kyc status | String | no | String
traits.customer.kyc.statusCode | status code | String | no | String 
traits.customer.kyc.lastVerified | last verified | long | no | 2023-12-05
traits.customer.kyc.claims | kyc claims | Object | no | Object
auth | auth info | Object | no | Object
auth.status | auth status | String | no | String  
auth.lastLoginAt | last login | long | no | long
auth.failedLogins | failed logins | int | no | 2

## verification

verification collection stores verification related all aspects while user creation and verification.

### example 

```json
{
  "_id": "656ef6f5e04a1c5726d26c63",
  "createdDate": "2023-12-05T10:09:57.382Z",
  "email": "test11@gmail.com",
  "emailOTP": "9767",
  "emailOTPExpriedDate": "2023-12-05T10:10:57.382Z",
  "emailVerified": true,
  "firstName": "Test",
  "lastName": "User",
  "phone": "9876547896",
  "phoneOTP": "2910",
  "phoneOTPExpriedDate": "2023-12-05T10:11:12.315Z",
  "phoneVerified": true,
  "lastEvent": {
    "createDate": "2023-11-15T13:48:06.649Z",
    "eventType": "USER_EMAIL_VERIFICATION_INITIATED",
    "payload": "{\"emailId\":\"testuser.12334@gmail.com\",\"otp\":\"2358\",\"createDate\":\"2023-11-15T13:48:06.645+00:00\",\"expiredDate\":\"2023-11-15T13:49:06.645+00:00\"}",
    "routingKey": "user.email-verification-initiated"
  }
}
```

### visual

```puml
@startjson
{
  "_id": "656ef6f5e04a1c5726d26c63",
  "createdDate": "2023-12-05T10:09:57.382Z",
  "email": "test11@gmail.com",
  "emailOTP": "9767",
  "emailOTPExpriedDate": "2023-12-05T10:10:57.382Z",
  "emailVerified": true,
  "firstName": "Test",
  "lastName": "User",
  "phone": "9876547896",
  "phoneOTP": "2910",
  "phoneOTPExpriedDate": "2023-12-05T10:11:12.315Z",
  "phoneVerified": true,
  "lastEvent": {
    "createDate": "2023-11-15T13:48:06.649Z",
    "eventType": "USER_EMAIL_VERIFICATION_INITIATED",
    "payload": "{\"emailId\":\"testuser.12334@gmail.com\",\"otp\":\"2358\",\"createDate\":\"2023-11-15T13:48:06.645+00:00\",\"expiredDate\":\"2023-11-15T13:49:06.645+00:00\"}",
    "routingKey": "user.email-verification-initiated"
  }
}
@endjson
```

### dictionary

field | description | characteristics | is enum | example
------|-------------|-----------------|---------|--------
_id | object id | ObjectId | no | 6554cc16ce74ee253e46db44
firstName | First Name | String | no | Test
lastName | Last Name | String | no | User
email | email | String | no | test@gmail.com
emailOTP  | otp | String | no | 9767
isEmailVerified | if email verified | boolean | no | true
emailOTPExpriedDate | otp expire date | Date | no | "2023-12-05T10:10:57.382Z"
phone | phone number | String | no | 9876007896
phoneOTP | otp | String | no | 2910
isPhoneVerified | if phone number verified | boolean | no | true
phoneOTPExpriedDate | otp expire date | Date | no | 2023-12-05T10:11:12.315Z
createdDate | created date | Date | no | 2023-12-05T10:09:57.382Z
lastEvent | last event | Object | no | Object
lastEvent.createdDate | created date | Date | no | 2023-11-15T13:48:06.649Z
lastEvent.eventType | event type | [EventType](https://gitlabnew.techwave.net/fintrust/af-commons/-/blob/main/src/main/java/com/fintrust/allfunds/commons/enums/EventType.java) | yes | USER_EMAIL_VERIFICATION_INITIATED
lastEvent.payLoad | payload | String | no | "{\"emailId\":\"testuser.12334@gmail.com\",\"otp\":\"2358\",\"createDate\":\"2023-11-15T13:48:06.645+00:00\",\"expiredDate\":\"2023-11-15T13:49:06.645+00:00\"}"
lastEvent.routingKey | routing key | String | no | user.email-verification-initiated

## scratchpad
scratchpad collection is used to store Items in cart, wishlist and compare.

### example

```json
{
  "_id": "52CF06LF",
  "cartItems": [
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF336L01PB2",
      "name": "HSBC Focused Fund - Direct Growth",
      "oneTimeOrSIP": {
        "amount": 5000,
        "investmentType": "ONETIME",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 0,
        "sipInterval": "",
        "sipIsPerpetual": true
      },
      "portfolioId": "02"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF680P01109",
      "name": "Shriram Flexi Cap Fund - Direct Growth",
      "oneTimeOrSIP": {
        "amount": 5000,
        "investmentType": "ONETIME",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 0,
        "sipInterval": "",
        "sipIsPerpetual": true
      },
      "portfolioId": "01"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF204K01G52",
      "name": "Nippon India Consumption Fund - Direct Plan Growth Plan - Growth Option",
      "oneTimeOrSIP": {
        "amount": 5000,
        "investmentType": "ONETIME",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 0,
        "sipInterval": "",
        "sipIsPerpetual": true
      },
      "portfolioId": "01"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF760K01DU1",
      "name": "CANARA ROBECO CONSUMER TRENDS FUND - DIRECT PLAN - GROWTH OPTION",
      "oneTimeOrSIP": {
        "amount": 2000,
        "investmentType": "SIP",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 1,
        "sipEndDate": "2024-05-01T00:00:00.000Z",
        "sipInterval": "MONTHLY",
        "sipIsPerpetual": true,
        "sipStartDate": "2023-12-01T00:00:00.000Z"
      },
      "portfolioId": "01"
    }
  ],
  "compareItems": [],
  "uccCode": "52CF06LF",
  "wishlistItems": [
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF760K01JC6",
      "name": "CANARA ROBECO SMALL CAP FUND - DIRECT PLAN - GROWTH OPTION"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF879O01100",
      "name": "Parag Parikh Tax Saver Fund- Direct Growth"
    },
    {
      "assetCategory": "Flexi Cap",
      "isin": "INF680P01109",
      "name": "Shriram Flexi Cap Fund - Direct Growth"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF336L01NV5",
      "name": "HSBC Large & Mid Cap Fund - Direct Growth"
    }
  ]
}
```

### visual

```puml
@startjson
{
  "_id": "52CF06LF",
  "cartItems": [
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF336L01PB2",
      "name": "HSBC Focused Fund - Direct Growth",
      "oneTimeOrSIP": {
        "amount": 5000,
        "investmentType": "ONETIME",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 0,
        "sipInterval": "",
        "sipIsPerpetual": true
      },
      "portfolioId": "02"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF680P01109",
      "name": "Shriram Flexi Cap Fund - Direct Growth",
      "oneTimeOrSIP": {
        "amount": 5000,
        "investmentType": "ONETIME",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 0,
        "sipInterval": "",
        "sipIsPerpetual": true
      },
      "portfolioId": "01"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF204K01G52",
      "name": "Nippon India Consumption Fund - Direct Plan Growth Plan - Growth Option",
      "oneTimeOrSIP": {
        "amount": 5000,
        "investmentType": "ONETIME",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 0,
        "sipInterval": "",
        "sipIsPerpetual": true
      },
      "portfolioId": "01"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF760K01DU1",
      "name": "CANARA ROBECO CONSUMER TRENDS FUND - DIRECT PLAN - GROWTH OPTION",
      "oneTimeOrSIP": {
        "amount": 2000,
        "investmentType": "SIP",
        "oneTimeTenureInMonths": 0,
        "sipDayOfMonth": 1,
        "sipEndDate": "2024-05-01T00:00:00.000Z",
        "sipInterval": "MONTHLY",
        "sipIsPerpetual": true,
        "sipStartDate": "2023-12-01T00:00:00.000Z"
      },
      "portfolioId": "01"
    }
  ],
  "compareItems": [],
  "uccCode": "52CF06LF",
  "wishlistItems": [
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF760K01JC6",
      "name": "CANARA ROBECO SMALL CAP FUND - DIRECT PLAN - GROWTH OPTION"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF879O01100",
      "name": "Parag Parikh Tax Saver Fund- Direct Growth"
    },
    {
      "assetCategory": "Flexi Cap",
      "isin": "INF680P01109",
      "name": "Shriram Flexi Cap Fund - Direct Growth"
    },
    {
      "assetCategory": "MIDCAP",
      "assetClass": "EQUITY",
      "isin": "INF336L01NV5",
      "name": "HSBC Large & Mid Cap Fund - Direct Growth"
    }
  ]
}
@endjson
```

### dictionary

field | description | characteristics | is enum | example
------|-------------|-----------------|---------|---------
_id | identifier | String | no | 52CF06LF
uccCode | user identity | String | no | 52CF06LF
wishlistItems | wishlist items | Array | no | Array of Objects
wishlistItems.isin | fund isin | String | no | INF760K01DU1
wishlistItems.name | fund name | String | no | Parag Parikh Tax Saver Fund- Direct Growth
wishlistItems.assetClass | asset class | [AssetClassType](https://gitlabnew.techwave.net/fintrust/af-commons/-/blob/main/src/main/java/com/fintrust/allfunds/commons/enums/AssetClassType.java) | yes | EQUITY
wishlistItems.assetCategory | asset category | String | no | MIDCAP
compareItems | compare items | Array | no | Array of Objects
compareItems.isin | fund isin | String | no | INF879O01100
compareItems.assetClass | asset class | [AssetClassType](https://gitlabnew.techwave.net/fintrust/af-commons/-/blob/main/src/main/java/com/fintrust/allfunds/commons/enums/AssetClassType.java) | yes | EQUITY
cartItems | cart items | Array | no | Array of Objects
cartItems.isin | fund isin | String | no | INF336L01NV5
cartItems.name | fund name | String | no | HSBC Focused Fund - Direct Growth
cartItems.assetClass | asset class | [AssetClassType](https://gitlabnew.techwave.net/fintrust/af-commons/-/blob/main/src/main/java/com/fintrust/allfunds/commons/enums/AssetClassType.java) | yes | EQUITY
cartItems.assetCategory | asset category | String | no | MIDCAP
cartItems.oneTimeOrSIP | purchase or sip or swp or stp or switch or redeem | Object | no | Object
cartItems.oneTimeOrSIP.oneTimeTenureInMonths | tenure in month | int32 | no | 12
cartItems.oneTimeOrSIP.sipDayOfMonth | day of the month | int32 | no | 1
cartItems.oneTimeOrSIP.amount | amount | Double | no | 5000
cartItems.oneTimeOrSIP.investmentType | investment type | String | no | BUY
cartItems.oneTimeOrSIP.sipStartDate | SIP start date | Date | no | 2023-12-01T00:00:00.000Z
cartItems.oneTimeOrSIP.sipEndDate | SIP end date | Date | no | 2024-05-01T00:00:00.000Z
cartItems.oneTimeOrSIP.sipInterval | SIP interval | String | no | MONTHLY
cartItems.oneTimeOrSIP.sipIsPerpetual | if SIP perpetual | boolean | no | true
cartItems.oneTimeOrSIP.transferTo | target fund | String | no | INF760K01DU1 
cartItems.oneTimeOrSIP.redeemOrSwitchOption | redeem option | String | no | E - All Units, A - Specific Amount, U - Specific Units
cartItems.oneTimeOrSIP.redeemOrSwitchUnits | number of units | String | no | 5
cartItems.oneTimeOrSIP.redeemOrSwitchAmount | amount | String | no | 500
cartItems.portfolioId | portfolio ID | String | no | 02
cartItems.folioId | folio ID | String | no | ABC
cartItems.bankAccountNo | back account number | String | no | 8762356784763
cartItems.isFormFilled | if form filled | boolean | no | true
cartItems.isPayoutChecked | if payout checked | boolean | no | false
meta | metadata | Object | no | Object
meta.created | created date| Date | no | 2023-12-05T10:11:12.315Z
meta.lastModified | last modified | Date | no | 2023-12-05T10:11:12.315Z
schemaVer | schema version | String | no | 1

## sfa_token

sfa_token collection stores sfa_token, User ID, device ID, fcm token etc.

### example

```json
{
  "_id": "65b8a2d4b99e8a50536a7121",
  "deviceId": "c2749b2874fcefd9",
  "expires": "2024-04-29T07:18:44.327Z",
  "fcmToken": "dwF-1wLtSQewAAHCBQksgc:APA91bEv_xmQwoycrG4V1k3rGm32JrEg0U2fbm2ig5JeRz8gwzErf8RTydC4uNKjgLwWUEs8p0SnDnTc-vid8MrPodfkuonycYKsjK7Rt0gtUTtBy7O7IBUgaPkfkPU178EzklQBfrrA",
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwczovL2V4YW1wbGUuY29tL21mQXV0aCIsInN1YiI6IlRRQkpYWlU3VlBXSiIsImdyb3VwcyI6WyJTRkEtVVNFUiJdLCJkZXZpY2VJRCI6ImMyNzQ5YjI4NzRmY2VmZDkiLCJpYXQiOjE3MDY1OTkxMjQsImV4cCI6MTcxNDM3NTEyNCwianRpIjoiODg5Mzc1MmEtOTI3Zi00OTg2LThiNmUtZTdhYTNmYWE0ZmEyIn0.M1lfgoqT8T8jvrW3woC7mkZxovZmyBFl9uEQULmu0696p_i8CRoHuzGeFdZn5d3s0n4_BsbDqSIiwhUlR0c8ghW-NldLSLW_geUUc72tl9M1LnWuM81ghgd-786RwemuUuOt7IzZsioziiuvihM7wDnuVK5N_AD2BD0ZHqPD9TukyjLBotGZKS2qoHdkhiqUmZ183_HWwVimZ7aqNK36XSCON17Gbf5typ6QRwbwwcV4kNVPwOR2OX4bhZ2lmQufgE-QOi70FI1P7KA8iEwNtjz3J87sHBXR5XY0u5P9pik0JMEjQCkxpFwTZ_kpkjUpdpaSCmjlWfxeMJarL2FI8A",
  "userAgent": "OnePlus OnePlus EB2101",
  "userId": "TQBJXZU7VPWJ"
}
```

### visual

```puml
@startjson
{
  "_id": "65b8a2d4b99e8a50536a7121",
  "deviceId": "c2749b2874fcefd9",
  "expires": "2024-04-29T07:18:44.327Z",
  "fcmToken": "dwF-1wLtSQewAAHCBQksgc:APA91bEv_xmQwoycrG4V1k3rGm32JrEg0U2fbm2ig5JeRz8gwzErf8RTydC4uNKjgLwWUEs8p0SnDnTc-vid8MrPodfkuonycYKsjK7Rt0gtUTtBy7O7IBUgaPkfkPU178EzklQBfrrA",
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwczovL2V4YW1wbGUuY29tL21mQXV0aCIsInN1YiI6IlRRQkpYWlU3VlBXSiIsImdyb3VwcyI6WyJTRkEtVVNFUiJdLCJkZXZpY2VJRCI6ImMyNzQ5YjI4NzRmY2VmZDkiLCJpYXQiOjE3MDY1OTkxMjQsImV4cCI6MTcxNDM3NTEyNCwianRpIjoiODg5Mzc1MmEtOTI3Zi00OTg2LThiNmUtZTdhYTNmYWE0ZmEyIn0.M1lfgoqT8T8jvrW3woC7mkZxovZmyBFl9uEQULmu0696p_i8CRoHuzGeFdZn5d3s0n4_BsbDqSIiwhUlR0c8ghW-NldLSLW_geUUc72tl9M1LnWuM81ghgd-786RwemuUuOt7IzZsioziiuvihM7wDnuVK5N_AD2BD0ZHqPD9TukyjLBotGZKS2qoHdkhiqUmZ183_HWwVimZ7aqNK36XSCON17Gbf5typ6QRwbwwcV4kNVPwOR2OX4bhZ2lmQufgE-QOi70FI1P7KA8iEwNtjz3J87sHBXR5XY0u5P9pik0JMEjQCkxpFwTZ_kpkjUpdpaSCmjlWfxeMJarL2FI8A",
  "userAgent": "OnePlus OnePlus EB2101",
  "userId": "TQBJXZU7VPWJ"
}
@endjson
```

### dictionary

field | description | characteristics | is enum | example
------|-------------|-----------------|---------|----------
_id | identifier | ObjectId | no | 65b8a2d4b99e8a50536a7121
deviceId | device login id | String | no | c2749b2874fcefd9
expires | token expire time | Date | no | 2024-04-29T07:18:44.327Z
fcmToken | fire base cloud messaging token | String | no | dwF-1wLtSQewAAHCBQksgc:APA91bEv_xmQwoycrG4V1k3rGm32JrEg0U2fbm2ig5JeRz8gwzErf8RTydC4uNKjgLwWUEs8p0SnDnTc-vid8MrPodfkuonycYKsjK7Rt0gtUTtBy7O7IBUgaPkfkPU178EzklQBfrrA
token | sfa token | String | no | eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwczovL2V4YW1wbGUuY29tL21mQXV0aCIsInN1YiI6IlRRQkpYWlU3VlBXSiIsImdyb3VwcyI6WyJTRkEtVVNFUiJdLCJkZXZpY2VJRCI6ImMyNzQ5YjI4NzRmY2VmZDkiLCJpYXQiOjE3MDY1OTkxMjQsImV4cCI6MTcxNDM3NTEyNCwianRpIjoiODg5Mzc1MmEtOTI3Zi00OTg2LThiNmUtZTdhYTNmYWE0ZmEyIn0.M1lfgoqT8T8jvrW3woC7mkZxovZmyBFl9uEQULmu0696p_i8CRoHuzGeFdZn5d3s0n4_BsbDqSIiwhUlR0c8ghW-NldLSLW_geUUc72tl9M1LnWuM81ghgd-786RwemuUuOt7IzZsioziiuvihM7wDnuVK5N_AD2BD0ZHqPD9TukyjLBotGZKS2qoHdkhiqUmZ183_HWwVimZ7aqNK36XSCON17Gbf5typ6QRwbwwcV4kNVPwOR2OX4bhZ2lmQufgE-QOi70FI1P7KA8iEwNtjz3J87sHBXR5XY0u5P9pik0JMEjQCkxpFwTZ_kpkjUpdpaSCmjlWfxeMJarL2FI8A
userAgent | agent name | String | no | OnePlus OnePlus EB2101
userId | user Id | String | no | TQBJ-XZU7-VPWJ


## mfu_profiles

mfu_profiles collection user details against mfu profile.

### example 
```json
{
  "_id": "WGK4DJWN5OW2",
  "accounts": [
    {
      "accountNo": "2213038184",
      "accountType": "SB",
      "bankId": "485",
      "bankName": "Kotak Mahindra Bank Limited",
      "bankSeqNum": 1,
      "defaultAccountFlag": "Y",
      "ifscCode": "KKBK0007478",
      "micrCode": "500485003",
      "proofType": "LATEST_BANK_ACCOUNT_STATEMENT"
    }
  ],
  "can": "31348MJ003",
  "canStatus": "PE",
  "documents": [
    {
      "_id": "657ab1c1f953330ef69ae4bc",
      "documentType": "1#PC",
      "eventType": "AD",
      "fileName": "Screenshot_20231214_125703_AllFunds",
      "imageRefNo": "ECA23348BC003"
    },
    {
      "_id": "657ab37af953330ef69ae4c2",
      "documentType": "1#PC",
      "eventType": "AD",
      "fileName": "Screenshot_20231214_125703_AllFunds",
      "imageRefNo": "ECA23348BC005"
    }
  ],
  "nominees": [
    {
      "nomineeDob": "1993-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Prasad",
      "nomineeRelation": "Son",
      "nomineeSeqNum": 1,
      "percentage": "50"
    },
    {
      "nomineeDob": "1993-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Prasad",
      "nomineeRelation": "Son",
      "nomineeSeqNum": 1,
      "percentage": "50"
    },
    {
      "nomineeDob": "1997-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Kamal",
      "nomineeRelation": "Brother",
      "nomineeSeqNum": 2,
      "percentage": "40"
    },
    {
      "nomineeDob": "2023-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "2005-12-15",
      "nomineeGuardianName": "John",
      "nomineeGuardianRelation": "Uncle",
      "nomineeName": "Lewis",
      "nomineeRelation": "Monkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1996-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "2005-12-15",
      "nomineeGuardianName": "John",
      "nomineeGuardianRelation": "Uncle",
      "nomineeName": "Lewis",
      "nomineeRelation": "Monkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1996-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "2005-12-15",
      "nomineeGuardianName": "John",
      "nomineeGuardianRelation": "Uncle",
      "nomineeName": "Lewis",
      "nomineeRelation": "Monkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "2003-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Lewis",
      "nomineeRelation": "Donkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1986-05-04T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Hurch",
      "nomineeRelation": "Fried",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1986-05-04T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Hurch",
      "nomineeRelation": "Fried",
      "nomineeSeqNum": 2,
      "percentage": "100"
    }
  ]
}
```

### visual
```puml
@startjson
{
  "_id": "WGK4DJWN5OW2",
  "accounts": [
    {
      "accountNo": "2213038184",
      "accountType": "SB",
      "bankId": "485",
      "bankName": "Kotak Mahindra Bank Limited",
      "bankSeqNum": 1,
      "defaultAccountFlag": "Y",
      "ifscCode": "KKBK0007478",
      "micrCode": "500485003",
      "proofType": "LATEST_BANK_ACCOUNT_STATEMENT"
    }
  ],
  "can": "31348MJ003",
  "canStatus": "PE",
  "documents": [
    {
      "_id": "657ab1c1f953330ef69ae4bc",
      "documentType": "1#PC",
      "eventType": "AD",
      "fileName": "Screenshot_20231214_125703_AllFunds",
      "imageRefNo": "ECA23348BC003"
    },
    {
      "_id": "657ab37af953330ef69ae4c2",
      "documentType": "1#PC",
      "eventType": "AD",
      "fileName": "Screenshot_20231214_125703_AllFunds",
      "imageRefNo": "ECA23348BC005"
    }
  ],
  "nominees": [
    {
      "nomineeDob": "1993-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Prasad",
      "nomineeRelation": "Son",
      "nomineeSeqNum": 1,
      "percentage": "50"
    },
    {
      "nomineeDob": "1993-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Prasad",
      "nomineeRelation": "Son",
      "nomineeSeqNum": 1,
      "percentage": "50"
    },
    {
      "nomineeDob": "1997-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Kamal",
      "nomineeRelation": "Brother",
      "nomineeSeqNum": 2,
      "percentage": "40"
    },
    {
      "nomineeDob": "2023-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "2005-12-15",
      "nomineeGuardianName": "John",
      "nomineeGuardianRelation": "Uncle",
      "nomineeName": "Lewis",
      "nomineeRelation": "Monkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1996-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "2005-12-15",
      "nomineeGuardianName": "John",
      "nomineeGuardianRelation": "Uncle",
      "nomineeName": "Lewis",
      "nomineeRelation": "Monkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1996-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "2005-12-15",
      "nomineeGuardianName": "John",
      "nomineeGuardianRelation": "Uncle",
      "nomineeName": "Lewis",
      "nomineeRelation": "Monkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "2003-12-15T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Lewis",
      "nomineeRelation": "Donkey",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1986-05-04T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Hurch",
      "nomineeRelation": "Fried",
      "nomineeSeqNum": 2,
      "percentage": "100"
    },
    {
      "nomineeDob": "1986-05-04T00:00:00.000Z",
      "nomineeGuardianDob": "",
      "nomineeGuardianName": "",
      "nomineeGuardianRelation": "",
      "nomineeName": "Hurch",
      "nomineeRelation": "Fried",
      "nomineeSeqNum": 2,
      "percentage": "100"
    }
  ]
}
@endjson
```

### dictionary

fields | description | characteristics | is enum | example
-------|-------------|-----------------|---------|----------
_id | ucc id as identifier | String | no | WGK4-DJWN-5OW2
can | can (common account number) | String | no | 31348MJ003
canStatus | status of can | String | no | PE
nominees | nominees | Object | no| Object
nominees.nomineeSeqNum | sequence number | int | no | 1
nominees.nomineeName | nominee name | String | no | Prasad
nominees.nomineeRelation | relation | String | no | Son
nominees.percentage | percentage | String | no | 50
nominees.nomineeDob | nominee date of birth | Date | no | 1993-12-15T00:00:00.000Z
nominees.nomineeGuardianName | guardian name of nominee | String | no | John
nominees.nomineeGuardianRelation | relation with guardian | String | no | Uncle
nominees.nomineeGuardianDob | DOB of guardian of nominee | String | no | 2005-12-15
accounts | account details | Object | no | Object
accounts.bankSeqNum | sequence number of bank | int | no | 1
accounts.defaultAccountFlag | if default account number | String | no | Y
accounts.accountNo | account number | String | no | 2213038184
accounts.accountType | account type | String | no | SB
accounts.bankId | bank Id | String | no | 485
accounts.bankName | bank name | String | no | Kotak Mahindra Bank Limited
accounts.ifscCode | ifsc code | String | no | KKBK0007478
accounts.micrCode | micr code | String | no | 500485003
accounts.proofType | bank proof type | [BankProofType](https://gitlabnew.techwave.net/fintrust/af-profile/-/blob/main/src/main/java/com/fintrust/allfunds/profile/impl/enums/BankProofType.java) | yes | LATEST_BANK_ACCOUNT_STATEMENT
accounts.mandates | mandates | Object | no | Array of Mandates
accounts.mandates.mmrn | String | String | no | String
accounts.mandates.mmrnRegStatus | String | String | no | String
accounts.mandates.mmrnAggrStatus | String | String | no | String
accounts.mandates.prn | String | String | no | String
accounts.mandates.stratdate | start date | Date | no | Date
accounts.mandates.endDate | end date | Date | no | Date
accounts.mandates.maxAmount | maximum amount | long | no | long
accounts.mandates.registrationMode | registration mode | [RegistrationModeType](https://gitlabnew.techwave.net/fintrust/af-profile/-/blob/main/src/main/java/com/fintrust/allfunds/profile/impl/enums/RegistrationModeType.java) | yes | PN
accounts.mandates.termsVersion | terms version | String | no | String
accounts.mandates.termsAgreed | if user agreed terms | boolean | no | true
accounts.mandates.termsAgreedDate | date of agreed terms | Date | no | Date
documents | document of proof | Object | no | Object
documents.id | identifier | Object Id | no | Object Id
documents.imageRefNo | image reference number | String | no | to be given
documents.fileName | name of file | String | no | to be given
documents.eventType | event type | String | no | to be given
documents.documentType | document type | String | no | to be given

## mfu_requests
mfu_requests collection stores payload details for mfu response.

### example
to be given
### visual
to be given
### dictionary
field | description | characteristics | is enum | example
------|-------------|-----------------|---------|---------
_id | identifier | ObjectId | no | to be given
orderId | order id | String | no | to be given
request | request | String | no | to be given
mfuResponse | mfu response | Object | no | Object
mfuResponse.statusCode | status code | int | no | to be given
mfuResponse.statusText | status text | String | no | to be given
mfuResponse.responseBody | response body |  String | no | to be given
sentAt | request sent date and time | long | no | to be given 
receivedAt | response revived date and time | Date | no | to be given 

## mfu_nct
mfu_nct collection stores details of non commercial transaction.

### example
to be given
 
### visual
to be given

### dictionary
fields | description | characteristics | is enum | example
-------|-------------|-----------------|---------|-------
_id | identifier | Object Id | no |to be given
ucc | unique customer code | String | no | to be given
changeType | change tye | String | no | to be given
operation | operation | String | no | to be given
sentAt | request date and time | Date | no | to be given
responserecievedAt | response date and time| Date | not | to be given
status | status | String | no | to be given
mfuStatus | mfu status | String | no | to be given
uniqueId | unique Id | String | no | to be given
nctRefNo | nct reference number | String | no | to be given
bankDetails | bank details | Object | no | Object
bankDetails.bankSeqNum | bank sequence number | int | no | to be given
bankDetails.defaultAccountFlag | if default account selected | boolean | no | to be given
bankDetails.accountNo | account number | String | no | to be given
bankDetails.accountType | account type | String | no | to be given
bankDetails.bankId | bank Id | String | no | to be given
bankDetails.bankName | bank name | String | no | to be given
bankDetails.ifscCode | ifsc code | String | no | to be given
bankDetails.micrCode | micr code | String | no | to be given
bankDetails.proofType | proof type | [BankProofType](https://gitlabnew.techwave.net/fintrust/af-profile/-/blob/main/src/main/java/com/fintrust/allfunds/profile/impl/enums/BankProofType.java) | yes | to be given
bankDetails.bankEventType | bank event type | [BankEventType](https://gitlabnew.techwave.net/fintrust/af-profile/-/blob/main/src/main/java/com/fintrust/allfunds/profile/impl/enums/BankEventType.java) | yes | to be given

## orders
orders collection stores all aspect of transaction apis of order like Purchase, SWP, STP, SWP, Redeem and Switch.

### example
```json
{
  "_id": "Z1B1LRY1O7VQGWMRY4LR",
  "can": "14167AZA01",
  "orderCreatedDate": "2024-02-01T09:22:29.660Z",
  "redeemItems": [
    {
      "accountNumber": "50200013404502",
      "amount": "1200.0",
      "assetClassType": "EQUITY",
      "folioId": "AZA011416727",
      "ifscCode": "HDFC0000090",
      "isin": "INF090I01742",
      "micrCode": "110240012",
      "name": "HDFC BANK LTD",
      "volumeType": "A"
    }
  ],
  "statusType": "CREATED",
  "transactionType": "REDEEM",
  "userId": "TQBJXZU7VPWJ"
}
```

### visual
```puml
@startjson
{
  "_id": "Z1B1LRY1O7VQGWMRY4LR",
  "can": "14167AZA01",
  "orderCreatedDate": "2024-02-01T09:22:29.660Z",
  "redeemItems": [
    {
      "accountNumber": "50200013404502",
      "amount": "1200.0",
      "assetClassType": "EQUITY",
      "folioId": "AZA011416727",
      "ifscCode": "HDFC0000090",
      "isin": "INF090I01742",
      "micrCode": "110240012",
      "name": "HDFC BANK LTD",
      "volumeType": "A"
    }
  ],
  "statusType": "CREATED",
  "transactionType": "REDEEM",
  "userId": "TQBJXZU7VPWJ"
}
@endjson
```

### dictionary
fields | description | characteristics | is enum | example
-------|-------------|-----------------|---------|----------
_id | external group order reference number as identifier | String | no | Z1B1-LRY1-O7VQ-GWMR-Y4LR
userId | all funds user Id | String | no | TQBJ-XZU7-VPWJ
can | common account number | String | no | 14167AZA01
portfolioId | portfolio Id | String | no | 01
mfuGroupOrderReferenceNumber | mfu group order reference number | String | no | to be given
orderCreatedDate | order created date | Date | no | 2024-02-01T09:22:29.660Z
orderSentDate | order sent date | Date | no | 2024-02-01T09:22:29.660Z
statusType | status type | [OrderStatusType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/OrderStatusType.java) | yes | CREATED
transactionType | transaction type | [TransactionType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/TransactionType.java) | yes | REDEEM
orderResponse | order response | Object | no | Object
orderResponse.txnRespCodeDetail | transaction response code detail | Object | no | Object
orderResponse.txnRespCodeDetail.errorFlag | error flag | String | no | to be given
orderResponse.txnRespCodeDetail.errorCode | error code | String | no | to be given
orderResponse.txnRespCodeDetail.errorMsg | error message | String | no | to be given
orderResponse.groupOrderNo | group order no | String | no | to be given
orderResponse.orderDate | order date | String | no | to be given
orderResponse.lastModifiedDate | last modified date | String | no | to be given
orderResponse.lastModifiedTime | last modified time | String | no | to be given
orderResponse.paymentFlag | payment flag | String | no | to be given
orderResponse.submitToPosFlag | to be given | String | no | to be given
orderResponse.txnApproveFlag | transaction approve flag | String | no | to be given
orderResponse.bankRefFlag | bank reference flag | String | no | to be given
orderResponse.bankTxnRefNo | bank transaction reference number | String | no | to be given
orderResponse.virtualAccNo | virtual account number | String | no | to be given
orderResponse.virtAccIfsc | virtual account ifsc | String | no | to be given
orderResponse.appLinkPrim | app link primary | String | no | to be given
orderResponse.appLinkH1 | to be given | String | no | to be given
orderResponse.appLinkH2 | to be given | String | no | to be given
orderResponse.appLinkPOA | to be given | String | no | to be given
orderResponse.netBankingLink | net banking link | String | no | to be given
orderResponse.payItrnSplitList | to be given | Array of Objects | no | Array of Objects
orderResponse.payItrnSplitList.accName | account name | String | no | to be given
orderResponse.payItrnSplitList.accType | account type | String | no | to be given
orderResponse.payItrnSplitList.amcPayID | amc pay Id | String | no | to be given
orderResponse.payItrnSplitList.ifsc | ifsc code | String | no | to be given
orderResponse.payItrnSplitList.invAccNo | to be given | String | no | to be given
orderResponse.payItrnSplitList.itrn | to be given | String | no | to be given
orderResponse.payItrnSplitList.itrnAmt | to be given | String | no | to be given
orderResponse.payItrnSplitList.rtaAmcCode | rta amc code | String | no | to be given
orderResponse.payItrnSplitList.rtaSchCode | to be given | String | no | to be given
orderResponse.payItrnSplitList.uniqPayItrnRefNo | to be given | String | no | to be given
orderResponse.payItrnSplitList.usrTxnRefNo | to be given | String | no | to be given

## outbox
to be provided 

## portfolio
portfolio collection stores assets of a user.


### example
```json
{
  "_id": "65a11d232d810368f1df3bee",
  "custmerId": "H76C6ZRJV9VV",
  "distribution": {
    "commodity": 0,
    "debt": 40,
    "equity": 60
  },
  "draft": true,
  "investmentApproach": "Moderate",
  "meta": {
    "created": "1706078825523",
    "lastModified": "0",
    "schemaVer": "1"
  },
  "oneTimeOrSIP": {
    "amount": 50000,
    "investmentType": "ONETIME",
    "oneTimeTenureInMonths": 120,
    "sipDayOfMonth": 0,
    "sipIsPerpetual": false
  },
  "questions": [
    {
      "questionId": "1",
      "selectedOption": 2
    },
    {
      "questionId": "2",
      "selectedOption": 3
    },
    {
      "questionId": "3",
      "selectedOption": 2
    },
    {
      "questionId": "4",
      "selectedOption": 3
    },
    {
      "questionId": "5",
      "selectedOption": 3
    },
    {
      "questionId": "6",
      "selectedOption": 2
    },
    {
      "questionId": "7",
      "selectedOption": 3
    }
  ]
}
```


### visual
```puml
@startjson
{
  "_id": "65a11d232d810368f1df3bee",
  "custmerId": "H76C6ZRJV9VV",
  "distribution": {
    "commodity": 0,
    "debt": 40,
    "equity": 60
  },
  "draft": true,
  "investmentApproach": "Moderate",
  "meta": {
    "created": "1706078825523",
    "lastModified": "0",
    "schemaVer": "1"
  },
  "oneTimeOrSIP": {
    "amount": 50000,
    "investmentType": "ONETIME",
    "oneTimeTenureInMonths": 120,
    "sipDayOfMonth": 0,
    "sipIsPerpetual": false
  },
  "questions": [
    {
      "questionId": "1",
      "selectedOption": 2
    },
    {
      "questionId": "2",
      "selectedOption": 3
    },
    {
      "questionId": "3",
      "selectedOption": 2
    },
    {
      "questionId": "4",
      "selectedOption": 3
    },
    {
      "questionId": "5",
      "selectedOption": 3
    },
    {
      "questionId": "6",
      "selectedOption": 2
    },
    {
      "questionId": "7",
      "selectedOption": 3
    }
  ]
}
@endjson
```


### dictionary
fields | description | characteristics | is enum | example
-------|-------------|-----------------|---------|----------
_id | Id | Object | no | 65a907018919ff20f94ba57a
draft | if drafted | boolean | no | true
label | label name of portfolio | String | no | to be provided
custmerId | customer Id |  String | no | 52B5-50K0-L1ES
investmentApproach | investment approach | String | no | aggressive
distribution | distribution | Object | no | Object
distribution.commodity | asset distribution in commodity | int | no | 0
distribution.equity | asset distribution in equity | int | no | 60
distribution.debt | asset distribution in debt | int | no | 40
questions | array of questions | array of questions | no | array of questions
questions.selectedOption | selected option | int | no | 2
questions.questionId | question Id | String | no | 7
oneTimeOrSIP | one time or sip or swp or switch or redeem or buy | Object | no | Object
oneTimeOrSIP.oneTimeTenureInMonths | tenure in month | int | no | 12
oneTimeOrSIP.sipDayOfMonth | day of the month | int | no | 3
oneTimeOrSIP.amount | amount | Double | no | 5000
oneTimeOrSIP.investmentType | investment type | String | no | ONETIME
oneTimeOrSIP.sipStartDate | sip start date | Date | no | 2023-09-07T00:00:00.000Z
oneTimeOrSIP.sipEndDate | sip end date | Date | no | 2024-03-10T00:00:00.000Z
oneTimeOrSIP.sipInterval | sip interval | String | no | QUARTERLY
oneTimeOrSIP.sipIsPerpetual | sip is perpetual | boolean | no | true
meta | meta | Object | no | Object
meta.created | created at | int 64 | no | 1706078825523
meta.lastModified | last modified at | int 64 | no | 0
meta.schemaVer | schema version | String | no | 1

## transaction
transaction collection stores request and response of mfu orders and maintain transaction status.

### example

```json
{
  "_id": "ZZUG1EA2ZFE5K2NUF4WM",
  "executor": {
    "mfu": {
      "mfuItrnNo": "01",
      "orderId": "A98JHU9827JHF8726HI3"
    }
  },
  "isin": "INF204K01ZP3",
  "panNumber": "BTCPK4218U",
  "redeem": {
    "accountNumber": "1233",
    "ifscCode": "UTBI0BEC13",
    "micrCode": "123456789",
    "volumeType": "E"
  },
  "status": "FAILED",
  "transactionType": "REDEEM",
  "txDate": "2024-01-23T08:19:05.164Z",
  "userId": "JHMJDETS"
}
```
### visual

```puml
@startjson
{
  "_id": "ZZUG1EA2ZFE5K2NUF4WM",
  "executor": {
    "mfu": {
      "mfuItrnNo": "01",
      "orderId": "A98JHU9827JHF8726HI3"
    }
  },
  "isin": "INF204K01ZP3",
  "panNumber": "BTCPK4218U",
  "redeem": {
    "accountNumber": "1233",
    "ifscCode": "UTBI0BEC13",
    "micrCode": "123456789",
    "volumeType": "E"
  },
  "status": "FAILED",
  "transactionType": "REDEEM",
  "txDate": "2024-01-23T08:19:05.164Z",
  "userId": "JHMJDETS"
}
@endjson
```
### dictionary
fields | description | characteristics | is enum | example
-------|-------------|-----------------|---------|---------
_id | external transaction reference number as id | String | no | ZZUG-1EA2-ZFE5-K2NU-F4WM
isin | fund isin | String | no | INF204K01ZP3
userId | user Id | String | no | JHMJDETS
portfolioId | portfolio Id | String | no | 01
status | transaction status type | [TransactionStatusType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/TransactionStatusType.java) | yes | FAILED
transactionType | transaction type | [TransactionType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/TransactionType.java) | yes | REDEEM
txDate | transaction date | Date | no | 2024-01-23T08:19:05.164Z
panNumber | pan number | String | no | BTCPK4218U
accounting | accounting detail | Object | no | Object
accounting.remarks | remark | String | no | to be given
accounting.folioNumber | folio number | String | no | to be given
purchase | purchase details | Object | no | Object
purchase.tenureInMonths | tenure in month | int | no | to be given
purchase.amount | amount | decimal | no | 5000
sip | systematic investment plan details | Object | no | Object
sip.frequency | frequency | [FrequencyType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/FrequencyType.java) | yes | D
sip.day | day | String | no | 1
sip.startDate | start date | Date | no | to be given
sip.endDate | end date | Date | no | to be given
sip.amount | amount | Decimal | no | to be given
swp | systematic withdrawal plan details | Object | no | Object
swp.startDate | start date | Date | no | to be given
swp.endDate | end date | Date | no | to be given
swp.dayOfMonth | day of the month | Date | no | to be given 
swp.frequencyType | frequency type | [FrequencyType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/FrequencyType.java) | yes | D
swp.amount | amount | Decimal | no | 5000
stp | systematic transfer plan details | Object | no | Object
stp.tarIsin | target isin | String | no | to be given
stp.tarName | target fund name | String | no | to be given
stp.tarAssetClassType | asset class type | String | no | to be given
stp.frequency | frequency type | [FrequencyType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/FrequencyType.java) | yes | D
stp.day | day | String | no | 4
stp.startDate | start date | Date | no | to be given
stp.endDate | end date | Date | no | to be given
stp.amount | amount | Decimal | no | to be given
switchFund | switch | Object | no | Object
switchFund.tarIsin | target isin | String | no | to be given
switchFund.tarName | target fund name | String | no | to be given
switchFund.tarAssetClassType | target asset class type | [AssetClassType](https://gitlabnew.techwave.net/fintrust/af-commons/-/blob/main/src/main/java/com/fintrust/allfunds/commons/enums/AssetClassType.java) | no | EQUITY
switchFund.tarAssetCategory | target asset category | String | no | Large cap
switchFund.amount | amount | Decimal | no | to be given
switchFund.units | units | Decimal | no | to be given
switchFund.volumeType | volume type | [VolumeType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/VolumeType.java) | no | E
redeem | redeem | Object | no | Object
redeem.payoutFlag | payout flag | String | no | to be given
redeem.amount | redeem amount | Decimal | no | to be given
redeem.units | units | Decimal | no | to be given
redeem.volumeType | volume type | [VolumeType](https://gitlabnew.techwave.net/fintrust/af-portfolio/-/blob/main/src/main/java/com/fintrust/allfunds/portfolio/impl/enums/VolumeType.java) | no | to be given
redeem.accountNumber | account number | String | no | to be given
redeem.ifscCode | ifsc code | String | no | to be given
redeem.micrCode | micr code | String | no | to be given
executor | executor | Object | no | Object
executor.mfu | mfu | Object | no | Object
executor.mfu.orderId | order Id | String | no | to be given
executor.mfu.mfuOrderRef | mfu order reference | String | no | to be given
executor.mfu.mfuItrnNo | mfu itr number | String |no | to be given
executor.mfu.mfuOrderDate | mfu order date | String | no | to be given
executor.mfu.mfuStatus | mfu status | String | no | to be given
executor.mfu.systematicCancel | systematic cancel | Object | no | to be given
executor.mfu.systematicCancel.mfuSCOrderId | mfu sc order id | String | no | to be given
executor.mfu.systematicCancel.mfuSCOrderRef | mfu sc order ref | String | no | to be given
executor.mfu.systematicCancel.mfuSCOrderDate | mfu sc oder date | String | no | to be given
executor.mfu.systematicCancel.mfuLastModDate | mfu last mod date | String | no | to be given
executor.mfu.systematicCancel.mfuLastModTime | mfu last mod time | String | no | to be given

