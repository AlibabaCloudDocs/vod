# FAQ about event notifications

## How do I troubleshoot the failure to receive an HTTP callback notification?

-   In the ApsaraVideo VOD console, choose **Configuration Management** \> Media Processing \> **Callback** in the left-side navigation pane. On the Callback page, check whether you have enabled the callback feature and selected the required callback events.
-   If you have completed the preceding settings, run the following sample code to check whether a response is returned. If not, check whether the callback message receiving server works properly. Replace `http://sample.host.com/processMessage` with the callback URL for receiving HTTP messages.

    ```
    curl -l -i -H "Content-type: application/json" -X POST -d '{"VideoId":"videoId","EventType":"FileUploadComplete","Status":"success","Size":1439213}' http://sample.host.com/processMessage
    ```


## How long is the timeout period for an HTTP callback request? How many times does ApsaraVideo VOD resend the callback request upon a callback failure? How long is the retry interval?

-   By default, the timeout period for an HTTP callback request is 5 seconds. ApsaraVideo VOD resends the callback request up to three times at intervals of 1 second upon a callback failure.

## Is an HTTP callback request discarded when the number of retries exceeds the upper limit? How can I prevent message loss?

-   If your callback message receiving server fails to receive an HTTP callback request due to service interruption, service restart, or network connection failure, the HTTP callback request is discarded when the number of retries exceeds the upper limit. We recommend that you use the Message Service \(MNS\) callback method to prevent message loss.

## Is HTTP status code 302 supported?

-   The HTTP callback method supports only HTTP status code 200. Other HTTP status codes such as 301 and 302 are not supported for security reasons.

## Why does my server receive an HTTP callback request multiple times?

-   ApsaraVideo VOD considers that an HTTP callback is successful only when it receives HTTP status code 200. If the HTTP status code is not 200 or the callback times out, ApsaraVideo VOD considers that the callback fails and resends the callback request. ApsaraVideo VOD resends a callback request up to three times.

## What is HTTP authentication?

-   During HTTP authentication, ApsaraVideo VOD allows you to add a specific signature header to HTTP callback requests. The callback message receiving server verifies the signature to prevent illegal requests from requesters other than ApsaraVideo VOD. You can determine whether to enable HTTP authentication.

## MNS callback

## Why does no message exist in the MNS queue?

-   A message fails to be delivered to the MNS queue due to the following reasons: You do not authorize ApsaraVideo VOD to access MNS, the MNS endpoint in your submitted ticket is not a public endpoint, or the queue name is invalid.
-   If the time to live \(TTL\) of a message is too short, the message may have been released before it can be consumed. We recommend that you set the TTL to 3,600 seconds.
-   If the maximum message length is too short, the message may fail to be delivered to the MNS queue. We recommend that you use the default length 65,536 bytes.

## Why do I receive a message multiple times?

-   A message is invisible for a short period after it is consumed. You must delete the message manually or by calling an API operation. Otherwise, the message can be consumed again after that period.

## Does the MNS callback method support authentication?

-   ApsaraVideo VOD can deliver messages to the MNS queue only after it is authorized to access MNS. Compared with the HTTP callback method, the MNS callback method is more secure and does not require authentication.

## In which regions is the MNS callback method available?

-   If you store videos in a region in **mainland China**, such as the **China \(Beijing\)** region or **China \(Shanghai\)** region, we recommend that you use an MNS queue in the **China \(Shanghai\)** region because a short latency may exist when you deliver messages to a queue in other regions.
-   If you store videos in the **Singapore** region, we recommend that you use an MNS queue in the Singapore region.
-   If you store videos in the **Germany \(Frankfurt\)** region, we recommend that you use an MNS queue in the Germany \(Frankfurt\) region.

## Can I use an MNS queue for callback across regions?

-   Yes. For example, you can store and process videos in the China \(Shanghai\) region or China \(Beijing\) region and deliver messages to an MNS queue in the China \(Shenzhen\) region. However, message delivery may be delayed due to network latency. Therefore, we recommend that you deliver messages to an MNS queue in the region where your videos are stored.

