# **Set IP Blacklist**

## **1. Description**

Set the IP blacklist to make the IP unable to access the current accelerated domain.

## **2. Request Parameters**

| **Name**   | **Type** | **Compulsory or not** | **Description**                                                     |
| ---------- | -------- | ------------ | ------------------------------------------------------------ |
| username   | String   | Yes           | JD User Name pin                                                |
| signature  | String   | Yes           | User signature, verify user's identity information through md5 method to ensure information security. </br>md5=date+username+secret key SecretKey; date: format is yyyymmdd; username: JD user name pin; secret key: agreed between the Parties; </br>example: such as current date 2016-10-23, user pin: jcloud_00, user secret key SecretKey: e7a31b1c5ea0efa9aa2f29c6559f7d61, then the signature is MD5(20161023jcloud_00e7a31b1c5ea0efa9aa2f29c6559f7d61)|
| domain     | String   | Yes           | Accelerated Domain|
|iplist | String   | Yes           |IP blacklist, separated by English comma, up to 50 unrepeated ips can be added |

## **3. Return Parameters**

| **Name**   | **Description** | 
| ---------- | -------- |
| status  | It means whether the API request is successful or not, 0 means successful, any other number means failure  | 
| msg  | Notification Information | 
| data | Return Data| 

## **4. Call Example**

- ### **Request Address**

https://opencdn.jcloud.com/api/setIpBlackList

- ### **Request Example**

```
{
    "username": "user_test",
    "signature": "ca4c56f85e3582f4d814cc77949c82a7",
    "domain":"test.jcloud.com",
    "ipList":[
        "1.1.1.1",
        "2.2.2.2"
        ]
}
```

- ### **Return Example**

```
{
    "status": 0,
    "msg": "Succeeded",
    "data": "test.jcloud.com"
    }
}
```
