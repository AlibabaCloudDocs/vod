# Enable HTTPS secure acceleration

This topic describes the benefits and usage notes of HTTPS secure acceleration and how it works. This topic also describes the procedure for enabling HTTPS secure acceleration. HTTPS secure acceleration encrypts HTTPS connections between clients and Content Delivery Network \(CDN\) nodes. It ensures data security during transmission.

HTTP transmits data in plaintext and does not encrypt data in any form. As an extension of HTTP, HTTPS is an HTTP channel that is designed to ensure data security. In HTTPS, the communication protocol is encrypted by using Transport Layer Security \(TLS\) or Secure Sockets Layer \(SSL\). HTTPS supports authenticated and encrypted connections. Therefore, it is widely used to transmit sensitive data, such as transactions, over the Internet.

## How it works

After you enable HTTPS in the Alibaba Cloud CDN console, requests that are transmitted from clients to Alibaba Cloud CDN nodes are encrypted over HTTPS. CDN nodes retrieve requested resources from origin servers and then return the resources to clients over the protocol that is used by the origin servers. We recommend that you configure and enable HTTPS for your origin server to implement end-to-end HTTPS encryption.

The following figure shows the encryption process of HTTPS.

![Flowchart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3946219951/p47884.png)

1.  The client sends an HTTPS request.
2.  The server generates a public key and a private key. You can prepare the keys on your own or request them from a professional organization.
3.  The server sends the public key to the client.
4.  The client authenticates the certificate.

    -   If the certificate is valid, the client generates a random number as a key. The client uses the public key to encrypt the random number and transmits the random number to the server.
    -   If the certificate is invalid, the SSL handshake fails.
    **Note:** A valid certificate must meet the following requirements: The certificate has not expired. The certificate is issued by a trusted certificate authority \(CA\). The digital signature of the issuer in the certificate can be decrypted with the public key of the issuer. The domain name in the certificate is the same as that of the server.

5.  The server uses the private key to decrypt the random number.
6.  The server uses the random number to encrypt data and transmits the data to the client.
7.  The client uses the random number to decrypt the received data.

## Benefits

HTTPS secure acceleration has the following benefits:

-   HTTPS secure acceleration prevents communications from eavesdropping, tampering, impersonation attacks, and man-in-the-middle \(MITM\) attacks.
-   HTTPS encrypts sensitive information such as session IDs and cookies before transmission. This minimizes the risk of sensitive information leaks.
-   HTTPS checks data integrity during transmission to protect the data from MITM attacks, such as DNS hijacking and tampering.
-   HTTPS is the new standard. An increasing number of mainstream browsers such as Google Chrome 70 and later and Mozilla Firefox have labeled HTTP web URLs as not secure since 2018. If you choose to use HTTP, your website may be exposed to security risks. Users who visit your website by using these browsers are prompted that this website is not secure. This compromises user experience and may reduce visits to the website.
-   Mainstream browsers prioritize HTTPS web URLs in the search results. Additionally, mainstream browsers must support HTTPS before they can support HTTP/2. HTTPS is a more reliable choice in terms of security, market share, and user experience. Therefore, we recommend that you upgrade your communication protocol to HTTPS.

## Scenarios

The following table describes the scenarios of HTTPS secure acceleration.

|Scenario|Description|
|--------|-----------|
|Enterprise applications|HTTPS protects confidential information on enterprise websites from being hijacked or intercepted. Confidential information, such as customer relationship management \(CRM\) data and enterprise resource planning \(ERP\) data, is protected during transmission.|
|Government websites|HTTPS protects sensitive information on government websites against attacks such as phishing and hijacking. Leaks of such information may compromise public trust.|
|Payment systems|HTTPS protects sensitive data such as customer names and phone numbers used in payment transactions against hijacking and spoofing attacks. If sensitive data is leaked, attackers can use such data for fraudulent activities. This causes losses to both the customer and the enterprise.|
|API operations|API operations can use HTTPS to encrypt important information, such as sensitive data and important instructions. This protects the information against hijacking.|
|Enterprise websites|HTTPS improves user trust and experience. Web browsers display a lock icon in the address bar for websites with domain validated \(DV\) or organization validated \(OV\) certificates. The enterprise name is displayed together with the lock icon for websites that include extended validated \(EV\) certificates.|

1.  Purchase a certificate from [Alibaba Cloud SSL Certificates Service](https://common-buy.aliyun.com/?spm=5176.doc27118.2.9.u2oPum&commodityCode=cas#/buy).

    To enable HTTPS secure acceleration, you must own a certificate that corresponds to the domain name for CDN. You can apply for a free certificate or purchase an advanced certificate from **Alibaba Cloud SSL Certificates Service**.![Free certificates](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0785068061/p172540.png)

2.  Configure an HTTPS certificate.

    1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

    2.  In the left-side navigation pane of the ApsaraVideo VOD console, find **Configuration Management**.

    3.  Choose **CDN Configuration** \> **Domain Names**. The Domain Names page appears.

    4.  Find the domain name that you want to configure and click **Configure**.

        ![Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

    5.  Click **HTTPS**.

    6.  Click **Modify** in the **HTTPS Certificate** section.

        ![Modify the configuration of HTTPS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1785068061/p184294.png)

    7.  Modify the configuration.

        ![HTTPS Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1785068061/p184300.png)

        The following table describes the parameters.

        |Parameter|Description|
        |---------|-----------|
        |**Certificate Type**|        -   **Alibaba Cloud SSL Certificates Service**

You can apply for SSL certificates of various providers and types in the [SSL Certificates Service console](https://yundun.console.aliyun.com/?spm=5176.8232292.domaindetail.24.9498142fSMfoJd&p=cas#/cas/home).

After you apply for a free certificate, set the **Certificate Type** parameter to **Alibaba Cloud SSL Certificates Service** and select the free certificate.

            -   Free SSL certificates are typically issued within one to two business days. During this period of time, you can upload a custom certificate or select a certificate from Alibaba Cloud SSL Certificates Service.

**Note:** After you submit the application, the certificate may be issued within several hours or two business days. The time it takes depends on the verification process that is required by the CA.

            -   A free SSL certificate is valid for one year. Before it expires, you do not need to apply for a new certificate each time you enable HTTPS acceleration. You must apply for a new certificate only if the current one has expired.
        -   **Others**

If you cannot find a suitable SSL certificate, upload a custom certificate. To upload a custom certificate, you must specify a certificate name and upload the certificate content and private key. The uploaded certificate is saved to SSL Certificates Service. You can check the certificate on the [SSL Certificates](https://yundun.console.aliyun.com/?spm=5176.2020520110.all.12.16df56a1u1IhI6&p=cas#/cas/home) page.

**Note:** If the certificate name you enter already exists in the system when you upload a custom certificate, you can modify the certificate name and upload the certificate again. |
        |**Certificate Name**|When the **Certificate Type** parameter is set to **Alibaba Cloud SSL Certificates Service** or **Others**, you must enter the certificate name.|
        |**Content**|When the **Certificate Type** parameter is set to **Others**, you must enter the certificate content. For more information, click **PEM Encoding Example** under the **Content** field.|
        |**Private Key**|When the **Certificate Type** parameter is set to **Others**, you must enter the private key. For more information, click **PEM Encoding Example** under the **Private Key** field.|

3.  Click **OK**.


After a certificate is uploaded, it takes effect within 1 minute. To verify that the HTTPS certificate takes effect, send HTTPS requests to access resources. If the URL is displayed with a lock icon in the address bar of the browser, HTTPS secure acceleration is working as expected.

![Test result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7946219951/p3701.png)

