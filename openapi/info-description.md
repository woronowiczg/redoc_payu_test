# Overview

With PayU, you will quickly activate payments on your website or mobile device.

We provide a full set of endpoints which allow you to create, capture, cancel and retrieve orders, perform payouts or download reports.

The following reference is intended for merchants and developers to facilitate the use of the PayU API 

## Testing

### Production environment 

For a basic integration, including only a redirection to PayU hosted payment page, it is perfectly enough to use the public test point of sale. However, if you would like to test a full set of endpoints, including e.g. refunds, consider registering for a sandbox account.

__Public test POS (point of sale)__

| Key name                       | Value                            |
|--------------------------------|---------------------------------:|
| POS ID (pos_id)                | 145227                           |
| OAuth protocol - client_id     | 145227                           |
| Second key (MD5)               | 13a980d4f851f3d9a1cfc792fb1f5e50 |
| OAuth protocol - client_secret | 12f071174cb7eb79d4aac5bc2f07563f |


### Sandbox environment

Sandbox is an almost identical copy of PayU production system. It can be used for integration and testing purposes.

__Public test POS (point of sale)__

Although it is best to create your own account to later be able to configure it as needed, you may also use a public sandbox test POS without registering:

| Key name                       | Value                            |
|--------------------------------|---------------------------------:|
| POS ID (pos_id)                | 300746                           |
| OAuth protocol - client_id     | 300746                           |
| Second key (MD5)               | b6ca15b0d1020e8094d9b5f8d163db54 |
| OAuth protocol - client_secret | 2ee86a66e5d97e3fadc400c9f19b065d |

The availability of the sandbox environment can be checked on the __<a href="https://status.snd.payu.com/" target="_blank">Status page</a>__.

__Test cards__

In order to test card payments on sandbox, please use credentials displayed on the __<a href="https://developers.payu.com/en/overview.html#sandbox" target="_blank">Overview</a>__ documentation page.



