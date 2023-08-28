# Overview

This reference is designed to assist you in effectively utilizing the PayU REST API to enhance your online payment capabilities. Whether you're running an e-commerce store or developing applications that require secure and seamless payment processing, our API offers a range of features to meet your needs.

Our API offers a comprehensive set of endpoints to empower you with full control over your payment processes. With these endpoints, you can seamlessly create, capture, cancel, and retrieve orders, conduct payouts, and access essential reports.

For more details on the integration, please refer to the official <b><a href="/docs/">PayU documentation</a></b>. It provides comprehensive explanations, code samples, and best practices for seamless integration of the PayU API into your applications.

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

Although it is best to <b><a href="https://registration-merch-prod.snd.payu.com/boarding/#/registerSandbox/" target="_blank">create your own account</a></b> to later be able to configure it as needed, you may also use a public sandbox test POS without registering:

| Key name                       |                            Value |
| ------------------------------ | -------------------------------: |
| POS ID (pos_id)                |                           300746 |
| OAuth protocol - client_id     |                           300746 |
| Second key (MD5)               | b6ca15b0d1020e8094d9b5f8d163db54 |
| OAuth protocol - client_secret | 2ee86a66e5d97e3fadc400c9f19b065d |

The availability of the sandbox environment can be checked on the <b><a href="https://status.snd.payu.com/" target="_blank">Status page</a></b>.

**Testing Card Payments**

In order to test card payments on sandbox, please use credentials displayed on the <b><a href="/docs/testing/sandbox/" target="_blank">Sandbox</a></b> documentation page.

<!-- Status Codes

> Below is a list of status codes sent by the PayU system. Some status codes may be sent with a more detailed message.

If you need for PayU technical support to investigate an unsuccessful API call, please **[contact us](https://poland.payu.com/pomoc/)** and provide the value of the `Correlation-Id` header returned in the response.

<table>
    <thead>
        <th>HTTP Status Code</th>
        <th>Status Code</th>
        <th>codeLiteral/statusDesc</th>
        <th>Description</th>
    </thead>
    <tbody>
        <tr>
            <td><b>200</b> OK</td>
            <td>SUCCESS</td>
            <td></td>
            <td>Request has been processed correctly.</td>
        </tr>
        <tr>
            <td><b>201</b> Created</td>
            <td>SUCCESS</td>
            <td></td>
            <td>Order with <code>payMethods</code> array with card token or BLIK auth code has been created.</td>
        </tr>
        <tr>
            <td rowspan='4'><b>302</b> Found</td>
            <td>SUCCESS</td>
            <td></td>
            <td>Request has been processed correctly. <code>redirectUri</code> is provided in the response Location header and in the response body (in JSON payload).</td>
        </tr>
        <tr>
            <td>WARNING_CONTINUE_REDIRECT</td>
            <td></td>
            <td>Request has been processed correctly. <code>redirectUri</code> is provided in the response, in the <code>Location</code> header and in the response body (in JSON payload). Applies to transparent integration, if order request contains <code>payMethods</code> with following payment type values: <b>orx</b>, <b>bnx</b>, <b>gbx</b>, <b>nlx</b>.</td>
        </tr>
        <tr>
            <td>WARNING_CONTINUE_3DS</td>
            <td></td>
            <td>3DS authorization is required. Redirect the buyer to perform 3DS authentication process.</td>
        </tr>
        <tr>
            <td>WARNING_CONTINUE_CVV</td>
            <td></td>
            <td>CVV/CVC authorization required. Call the OpenPayU.authorizeCVV() method described <b><a href="/docs/payment-flows/card-payments/text-form-data/" target="_blank">here</a></b>.</td>
        </tr>
        <tr>
            <td rowspan="23"><b>400</b> Bad request</td>
            <td>ERROR_SYNTAX</td>
            <td></td>
            <td>Incorrect request syntax. Supported format is JSON.</td>
        </tr>
        <tr>
            <td rowspan="18">ERROR_VALUE_INVALID</td>
            <td></td>
            <td>One or more required values are incorrect.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: INVALID_BLIK_CODE</td>
            <td>BLIK authorization code must have 6 digits.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: OPENPAYU_PAYMENT_CREATE_ BLOCKED_CHECKOUT_PAY_METHOD</td>
            <td>Chosen payment method is currently unavailable. Payment methods availability can be checked by using <b><a href="/docs/checkout/payment-methods-retrieve/" target="_blank">Payment Methods Retrieval</a></b> service.</td>
        </tr>
        <tr>
            <td><b>codeLiteral</b>: SINGLE_CLICK_DISABLED</td>
            <td><b><a href="/docs/tokenization/" target="_blank">Card token</a></b> storing service is not available.</td>
        </tr>
        <tr>
            <td><b>codeLiteral</b>: SINGLE_CLICK_RECURRING_DISABLED</td>
            <td><b><a href="/docs/payment-methods/card-methods/recurring/" target="_blank">Recurring payments</a></b> service not available.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: General MCP processing error</td>
            <td>General MCP processing error.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Fx Rate Table is outdated</td>
            <td>Fx Rate Table specified by <code>mcpFxTableId</code> is outdated.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: MCP is not supported for merchant</td>
            <td>MCP is not supported for merchant.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Rate is null</td>
            <td>Field <code>mcpRate</code> is empty.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Fx Table Id is null</td>
            <td>Field <code>mcpFxTableId</code> is empty.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Amount is null</td>
            <td>Field <code>mcpAmount</code> is empty.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Currency is null</td>
            <td>Field <code>mcpCurrency</code> is empty.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Partner Id is null</td>
            <td>Field <code>mcpPartnerId</code> is empty.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Invalid currency pair for given Fx Table</td>
            <td>Invalid currency pair specified by <code>mcpCurrency</code> and <code>currencyCode</code> for given Fx Table.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Invalid rate value for given Fx Table</td>
            <td>Invalid rate value specified by <code>mcpRate</code> for given Fx Table.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Invalid amount value for given Fx Table (amount was not calculated properly)</td>
            <td>Invalid amount value specified by <code>mcpAmount</code> for given Fx Table, amount was not calculated properly.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Currency is not supported</td>
            <td>Currency specified by <code>mcpCurrency</code> is not supported.</td>
        </tr>
        <tr>
            <td><b>statusDesc</b>: Wrong params. You're trying to send MIT/Recurring request for non-verified first Payment</td>
            <td>MIT/recurring payment attempt with a token that has not been fully authenticated with 3DSecure. With a given token, depending on the payment type, you must first make a payment with the appropriate parameter: MIT (<code>cardOnFile=FIRST</code>), recurring (<code>recurring=FIRST</code>).</td>
        </tr>
        <tr>
            <td>ERROR_VALUE_MISSING</td>
            <td></td>
            <td>One or more required values are missing.</td>
        </tr>
        <tr>
            <td>ERROR_ORDER_NOT_UNIQUE</td>
            <td></td>
            <td>Order already exists. This error may be caused by a not unique <code>extOrderId</code> parameter.</td>
        </tr>
        <tr>
            <td>ERROR_INTERNAL</td>
            <td><b>codeLiteral</b>: CARD_CARD_EXPIRED</td>
            <td>Card expired.</td>
        </tr>
        <tr>
            <td>BUSINESS_ERROR</td>
            <td><b>codeLiteral</b>: ERROR_VALUE_INVALID <br/> <b>statusDesc</b>: Order was rejected by antifraud system</td>
            <td>Order was rejected by antifraud system.</td>
        </tr>
        <tr>
            <td><b>401</b> Unauthorized</td>
            <td>UNAUTHORIZED</td>
            <td></td>
            <td>Incorrect authentication. Check signature parameters and implementation of the signature algorithm</td>
        </tr>
        <tr>
            <td rowspan="2"><b>403</b> Forbidden</td>
            <td>UNAUTHORIZED_REQUEST</td>
            <td></td>
            <td>No privileges to perform the request</td>
        </tr>
        <tr>
            <td>ERROR_VALUE_INVALID</td>
            <td><b>codeLiteral</b>: INVALID_AUTH_FOR_THIS_ORDER</td>
            <td>POS ID parameter in OAuth request does not match <code>posId</code> in OrderCreateRequest. Both values must be the same.</td>
        </tr>
        <tr>
            <td><b>404</b> Not found</td>
            <td>DATA_NOT_FOUND</td>
            <td></td>
            <td>Data indicated in the request is not available in the PayU system.</td>
        </tr>
        <tr>
            <td><b>408</b> Request timeout</td>
            <td>TIMEOUT</td>
            <td></td>
            <td>Permitted time to process the request has expired.</td>
        </tr>
        <tr>
            <td rowspan="4"><b>500</b> Internal server error</td>
            <td>BUSINESS_ERROR</td>
            <td></td>
            <td>PayU system is unavailable. Try again later.</td>
        </tr>
        <tr>
            <td>ERROR_INTERNAL</td>
            <td></td>
            <td>PayU system is unavailable. Try again later.</td>
        </tr>
        <tr>
            <td>GENERAL_ERROR</td>
            <td></td>
            <td>Unexpected error. Try again later.</td>
        </tr>
        <tr>
            <td>WARNING</td>
            <td></td>
            <td>Minor unexpected error. Try again later.</td>
        </tr>
        <tr>
            <td><b>503</b> Service unavailable</td>
            <td>SERVICE_NOT_AVAILABLE</td>
            <td></td>
            <td>PayU system is unavailable. Try again later.</td>
        </tr>
    </tbody>
</table-->

<!--## Card Status Codes

**Reason** column shows which side stopped the transaction and who should be contacted to give more information about the source of problem.

<table>
    <thead>
        <tr>
            <td>Card ResponseCode</td>
            <td>Card ResponseCodeDesc</td>
            <td>Reason</td>
            <td>Additional information</td>
            <td>Public communication</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>000</td>
            <td>000 - OK</td>
            <td></td>
            <td></td>
            <td><b>Successful authorization</b>. Funds were transferred to the
            recipient.</td>
        </tr>
        <tr>
            <td>S01</td>
            <td>S01 - Refer to card issuer</td>
            <td>Bank</td>
            <td></td>
            <td rowspan="3"><b>Authorization error</b>. We are sorry, but your card's issuer rejected this
            transaction. If you would like to learn about the reason for this transaction to be
            rejected, please contact your bank. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>S04</td>
            <td>S04 - Pickup card</td>
            <td>Bank</td>
            <td></td>
        </tr>
        <tr>
            <td>S05</td>
            <td>S05 - Do not honor</td>
            <td>Bank</td>
            <td>Ask yor Customer to call the bank and clear up any problems that are causing
            the card to be declined.</td>
        </tr>
        <tr>
            <td>S12</td>
            <td>S12 - Invalid transaction</td>
            <td>Bank</td>
            <td></td>
            <td><b>No authorization</b>. We are sorry, but your card's issuer rejected this
            transaction. Check if you can use your card to pay online or contact your bank.
            Please try again, choosing a different payment method.</td>
        </tr>
        <tr>
            <td>S13</td>
            <td>S13 - Invalid amount</td>
            <td>Bank</td>
            <td>Currency conversion field overflow or amount exceeds maximum for Card
            program.</td>
            <td><b>No authorization</b>. We are sorry, but your card's issuer rejected this
            transaction. Check your card's limits or contact your bank. Please try again,
            choosing a different payment method.</td>
        </tr>
        <tr>
            <td>S30</td>
            <td>S30 - Message format error</td>
            <td>Bank</td>
            <td></td>
            <td rowspan="2"><b>Authorization error</b>. We are sorry, but your card's issuer rejected this
            transaction. If you would like to learn about the reason for this transaction to be
            rejected, please contact your bank. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>S43</td>
            <td>S43 - Pickup card (stolen card)</td>
            <td>Bank</td>
            <td></td>
        </tr>
        <tr>
            <td>S51</td>
            <td>S51 - Insufficient funds</td>
            <td>Bank</td>
            <td>Not enough funds or attempt to exceed limits (at the bank side).</td>
            <td><b>Insufficient funds</b>. Check funds available on your card or contact your
            bank. Please try again, choosing a different payment method.</td>
        </tr>
        <tr>
            <td>S54</td>
            <td>S54 - Expired card</td>
            <td>Bank</td>
            <td>Card is expired or Customer made a mistake giving card dates.</td>
            <td><b>No authorization</b>. We are sorry, but your card's issuer rejected this
            transaction. Check your card's expiration date or contact your bank. Please try
            again, choosing a different payment method.</td>
        </tr>
        <tr>
            <td>S57</td>
            <td>S57 - Card disabled for e-commerce or cross-border transactions</td>
            <td>Bank</td>
            <td></td>
            <td><b>No authorization</b>. We are sorry, but your card's issuer rejected this
            transaction. Check if you can use your card to pay online or contact your bank.
            Please try again, choosing a different payment method.</td>
        </tr>
        <tr>
            <td>S61</td>
            <td>S61 - Exceeds approval amount</td>
            <td>Bank</td>
            <td>Attempt to exceed limits (at the bank side).</td>
            <td></td>
        </tr>
        <tr>
            <td>S62</td>
            <td>S62 - Restricted card / Country exclusion table</td>
            <td>Bank</td>
            <td></td>
            <td><b>Authorization error</b>. We are sorry, but your card's issuer rejected this
            transaction. If you would like to learn about the reason for this transaction to be
            rejected, please contact your bank. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>S65</td>
            <td>S65 - Exceeds withdrawal frequency limit.</td>
            <td>Bank</td>
            <td></td>
            <td><b>Authorization error</b>. We are sorry, but your card's issuer rejected this
            transaction. If you would like to learn about the reason for this transaction to be
            rejected, please contact your bank. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>S89</td>
            <td>S89 - S89 - No such issuer</td>
            <td>Bank</td>
            <td>Attempt (bank side) to exceed the limit.</td>
            <td><b>No authorization</b>. We are sorry, but your card's issuer rejected this transaction. Check the limit settings on your card or contact your bank. Please try again using a different payment method.</td>
        </tr>
        <tr>
            <td>S90</td>
            <td>S90 - Destination not available</td>
            <td>Bank</td>
            <td></td>
            <td><b>Authorization error</b>. We are sorry, but your card's issuer rejected this
            transaction. If you would like to learn about the reason for this transaction to be
            rejected, please contact your bank. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>S93</td>
            <td>S93 - Card disabled for e-commerce transactions</td>
            <td>Bank</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>S99</td>
            <td>S99 - authorization error – default</td>
            <td>Bank</td>
            <td></td>
            <td rowspan="5"><b>Authorization error</b>. We are sorry, but your card's issuer rejected this
            transaction. If you would like to learn about the reason for this transaction to be
            rejected, please contact your bank. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>SN0</td>
            <td>SN0 - Unable to authorize / Force STIP</td>
            <td>Bank</td>
            <td></td>
        </tr>
        <tr>
            <td>SSD</td>
            <td>SSD - Soft decline (strong authentication required)</td>
            <td>Bank</td>
            <td>Payment can be retried, but 3DS authentication must be used.</td>
        </tr>
        <tr>
            <td>ST3</td>
            <td>ST3 - Card not supported</td>
            <td>Bank</td>
            <td></td>
        </tr>
        <tr>
            <td>ST5</td>
            <td>ST5 - Card inactive or closed (updated information needed)</td>
            <td>Bank</td>
            <td>Payment can be retried, but card data needs to be updated (e.g. expiry
            date).</td>
        </tr>
        <tr>
            <td>ST8</td>
            <td>ST8 - Invalid account</td>
            <td>Bank</td>
            <td></td>
            <td><b>No authorization</b>. We are sorry, but your card's issuer rejected this
            transaction. Check if you can use your card to pay online or contact your bank.
            Please try again, choosing a different payment method.</td>
        </tr>
        <tr>
            <td>SP1</td>
            <td>SP1 - Over daily limit (try again later)</td>
            <td>Bank</td>
            <td>Payment can be retried, preferrably after 24 hours.</td>
            <td rowspan="3"><b>Authorization error</b>. We are sorry, but your card's issuer rejected this
            transaction. If you would like to learn about the reason for this transaction to be
            rejected, please contact your bank. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>SAC</td>
            <td>SAC - Account closed (do not try again)</td>
            <td>Bank</td>
            <td>Payment must not be retried, all further attempts will be declined.</td>
        </tr>
        <tr>
            <td>SPF</td>
            <td>SPF - Possible fraud (do not try again)</td>
            <td>Bank</td>
            <td>Payment must not be retried, all further attempts will be declined.</td>
        </tr>
        <tr>
            <td>SP9</td>
            <td>SP9 - Enter lesser amount</td>
            <td>Bank</td>
            <td></td>
            <td><b>No authorization</b>. We are sorry, but your card's issuer rejected this
            transaction. Check your card's limits or contact your bank. Please try again,
            choosing a different payment method.</td>
        </tr>
        <tr>
            <td>114</td>
            <td>114 - 3ds authentication error (global)</td>
            <td>PayU</td>
            <td>Incorrect 3DS result (default configuration).</td>
            <td rowspan="5"><b>No authorization</b>. Your card's issuer did not confirm the
            transaction. Please try again.</td>
        </tr>
        <tr>
            <td>115</td>
            <td>115 - 3ds authentication error (company)</td>
            <td>PayU</td>
            <td>Incorrect 3DS result (company configuration).</td>
        </tr>
        <tr>
            <td>116</td>
            <td>116 - 3ds authentication error (merchant)</td>
            <td>PayU</td>
            <td>Incorrect 3DS result (merchant configuration).</td>
        </tr>
        <tr>
            <td>117</td>
            <td>117 - 3ds authentication error (fallback)</td>
            <td>PayU</td>
            <td>Incorrect 3DS result (fallback configuration).</td>
        </tr>
        <tr>
            <td>120</td>
            <td>120 - 3ds processing error</td>
            <td>PayU</td>
            <td>Error during 3DS processing.</td>
        </tr>
        <tr>
            <td>123</td>
            <td>123 - Missing cryptogram for Network Token's authorization.</td>
            <td>Visa/Mastercard</td>
            <td></td>
            <td><b>Authorization error</b>.
            We are sorry, but the attempt to confirm this transaction took too long. Please try again.</td>
        </tr>
        <tr>
            <td>130</td>
            <td>130 - Non-compliant prepaid card</td>
            <td>PayU</td>
            <td>Card recognized as not compliant with AMLD5.</td>
            <td><b>No authorization</b>. We are sorry, but this card is not accepted within the
            European Economic Area. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>131</td>
            <td>131 - Credit card not allowed for debt merchants</td>
            <td>PayU</td>
            <td>Card recognized as not allowed for this transaction.</td>
            <td><b>No authorization</b>. We are sorry, but credit card cannot be used to repay debt. Please try again, choosing a different payment
            method.</td>
        </tr>
        <tr>
            <td>222</td>
            <td>222 - Transaction not received by merchant</td>
            <td>Merchant</td>
            <td>Merchant has not received transaction; status possible when auto-receive option
            is off.</td>
            <td></td>
        </tr>
        <tr>
            <td>001, 002, 003, 004, 005, 110, 111, 112, 113, 121, 122, 221, 223, 998, 999</td>
            <td>different messages</td>
            <td>PayU</td>
            <td>Contact PayU for details</td>
            <td><b>Authorization error</b>.
            We are sorry, but the attempt to confirm this transaction took too long. Please try again.</td>
        </tr>
    </tbody>
</table -->

<!-- ## ECI (Electronic Commerce Indicator) Response Codes

<table>
    <thead>
        <th>cardEciCode</th>
        <th>Card Issuer</th>
        <th>Liable Party</th>
        <th>Chargeback Fraud Protection</th>
        <th>Additional Information</th>
    </thead>
    <tbody>
        <tr>
            <td>5 / 2</td>
            <td>Visa / Mastercard</td>
            <td>Issuer</td>
            <td>Protected</td>
            <td>Cardholder authenticated by the Issuer.</td>
        </tr>
        <tr>
            <td>6 / 1</td>
            <td>Visa / Mastercard</td>
            <td>Issuer</td>
            <td>Protected</td>
            <td>Merchant attempted to authenticate the cardholder but either the cardholder or Issuer is not participating in 3DS or the Issuer’s ACS is currently unavailable.</td>
        </tr>
        <tr>
            <td>7 / 0</td>
            <td>Visa / Mastercard</td>
            <td>Merchant</td>
            <td>Not Protected</td>
            <td>Payment authentication has not been performed.</td>
        </tr>
    </tbody>
    
</table>

## Card 3DS Statuses

<table>
    <thead>
        <th>card3DsStatus</th>
        <th>3DS version</th>
        <th>Additional information</th>
    </thead>
    <tbody>
        <tr>
            <td>AY / Y</td>
            <td>3DS / 3DS2</td>
            <td>Authentication successful.</td>
        </tr>
        <tr>
            <td>AA / A</td>
            <td>3DS / 3DS2</td>
            <td>Authentication attempted.</td>
        </tr>
        <tr>
            <td>AU / U</td>
            <td>3DS / 3DS2</td>
            <td>Authentication could not be performed due to technical or other problem.</td>
        </tr>
        <tr>
            <td>AN / N</td>
            <td>3DS / 3DS2</td>
            <td>Authentication failed. Authorization denied.</td>
        </tr>
        <tr>
            <td>VE</td>
            <td>3DS</td>
            <td>An error occurred during verification whether the card supports 3ds.</td>
        </tr>
        <tr>
            <td>AE</td>
            <td>3DS</td>
            <td>An error has occurred in the authentication process.</td>
        </tr>
        <tr>
            <td>R</td>
            <td>3DS2</td>
            <td>Authentication rejected. Authorization denied.</td>
        </tr>
        <tr>
            <td>I</td>
            <td>3DS2</td>
            <td>Informational status (the card issuer has accepted an exception to strong authentication).</td>
        </tr>
        <tr>
            <td>A0</td>
            <td>3DS</td>
            <td>Error on the card organization side.</td>
        </tr>
    </tbody>

</table> -->

<!-- ## Transmission Encryption

> Since 30 June 2018 PayU supports only TLS 1.2 protocol.

Lack of support for older protocols is for security reasons. The TLS 1.2 protocol is the best transmission encryption method compliant with the highest security standard PCI DSS 3.2.

**The change applies to all transmission via HTTPS, therefore it includes all REST API and Classic API endpoints.**

Majority of e-commerce solutions and hosting providers make sure that their software is up-to-date. Therefore, if your site is using such a provider, most probably you have nothing to worry about. You can contact your service providers and ask whether they have updated their software.

If your site is a custom-built solution, make sure that it uses the latest version of the protocol. The following information could be useful:

### JAVA

Java 1.5 and below does not support TLS 1.2 In Java 1.6, TLS 1.2 is not supported in Oracle public updates. It is supported in the business edition starting Oracle java version 6u115 b32.

In Java 1.7, TLS1.2 is supported. But it needs to be explicitly enabled by selecting the enabled protocols while creating the SSLSocket & SSLEngine instances.

Please refer to: <b><a href="https://blogs.oracle.com/java-platform-group/jdk-8-will-use-tls-12-as-default" target="_blank">Oracle blog</a></b> for more details.

### cURL

Curl supports TLS1.2 starting 7.34.0. Please use the following command to test the connection.

> You may use any PayU endpoint. If you need help with Classic API integration contact our <b><a href="https://poland.payu.com/support/" target="_blank">support</a></b>.


If it works, you'll see **Unauthorized** message.

### cURL+PHP

```
    php -r '$ch = curl_init(); 
    curl_setopt($ch, CURLOPT_URL, "https://secure.payu.com/api/v2_1/orders"); 
    curl_setopt ($ch, CURLOPT_SSLVERSION, 6); 
    var_dump(curl_exec($ch)); 
    var_dump(curl_error($ch));' 
```

If it works, you'll see "Unauthorized" message. TLS 1.1 and TLS 1.2 are supported since OpenSSL 1.0.1. Forcing TLS 1.1 and 1.2 are only supported since curl 7.34.0.

-->