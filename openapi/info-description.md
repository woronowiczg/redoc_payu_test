# Overview

This reference is designed to assist you in effectively utilizing the PayU REST API to enhance your online payment capabilities. Whether you're running an e-commerce store or developing applications that require secure and seamless payment processing, our API offers a range of features to meet your needs.

Our API offers a comprehensive set of endpoints to empower you with full control over your payment processes. With these endpoints, you can seamlessly create, capture, cancel, and retrieve orders, conduct payouts, and access essential reports.

For more details on the integration, please refer to the official <a href="/europe/docs/">PayU documentation</a>. It provides comprehensive explanations, code samples, and best practices for seamless integration of the PayU API into your applications.

## Testing

### Production Environment

For a basic integration, including only a redirection to PayU hosted payment page, it is perfectly enough to use the public test point of sale. However, if you would like to test a full set of endpoints, including e.g. refunds, consider registering for a sandbox account.

**Public Test POS (point of sale)**

| Key name                       |                            Value |
| ------------------------------ | -------------------------------: |
| POS ID (pos_id)                |                           145227 |
| OAuth protocol - client_id     |                           145227 |
| Second key (MD5)               | 13a980d4f851f3d9a1cfc792fb1f5e50 |
| OAuth protocol - client_secret | 12f071174cb7eb79d4aac5bc2f07563f |

### Sandbox Environment

Sandbox is an almost identical copy of PayU production system. It can be used for integration and testing purposes.

**Public Test POS (Point of Sale)**

Although it is best to <a href="https://registration-merch-prod.snd.payu.com/boarding/#/registerSandbox/" target="_blank">create your own account</a> to later be able to configure it as needed, you may also use a public sandbox test POS without registering:

| Key name                       |                            Value |
| ------------------------------ | -------------------------------: |
| POS ID (pos_id)                |                           300746 |
| OAuth protocol - client_id     |                           300746 |
| Second key (MD5)               | b6ca15b0d1020e8094d9b5f8d163db54 |
| OAuth protocol - client_secret | 2ee86a66e5d97e3fadc400c9f19b065d |

The availability of the sandbox environment can be checked on the <a href="https://status.snd.payu.com/" target="_blank">Status page</a>.

**Testing Card Payments**

In order to test card payments on sandbox, please use credentials displayed on the <a href="/europe/docs/testing/sandbox/" target="_blank">Sandbox</a> documentation page.