# Streaming Audio Files

## **Streaming Audio** <a id="streaming-audio"></a>

**To stream audio you need to build your own URL to call our streaming service**

`https://stream.svc.7digital.net/stream/catalogue`

**You need to pass in two parameters on the call**

| **Parameter** | Reason |
| :--- | :--- |
| `&shopId=2020` | To stream songs from the UMG catalog |
| `&trackId={int}` | The 7digital trackId of the song you want to stream |

**Most importantly you need to sign each call with Oauth 1.0 headers using the consumer key and secret provided for this hackathon**

* `consumer_key = 7d4vr6cgb392`
* `consumer_secret = m4ntskavq56rddsa`

**We have created a form to help build and sign streaming URLs**

* [`Click here - to access Oauth signature reference​`](http://7digital.github.io/oauth-reference-page/)
* `Do not use Postman - it does not correctly sign our URLs`

## ​[Oauth 1.0 Signature Reference Form](http://7digital.github.io/oauth-reference-page/)​ <a id="oauth-1-0-signature-reference-form"></a>

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LMw7rB6tN87JH_K_qhA%2F-LMxIOAhVEMF2ToTg9gb%2F-LMxJILHHdqnjdsy_EMo%2FScreen%20Shot%202018-09-21%20at%2019.07.26.png?alt=media&token=a82170cb-e275-4b2a-acc1-4c7e47d7306f)

**Instructions**

1. **Enter the streaming service URL as shown**
2. **Enter your consumer\_key & consumer\_secret**
3. **Enter shopId & trackId**
4. **Click \[refresh both\] button to sign API call with Oauth headers**
5. **Click URL to test stream**

## Partial Streams <a id="partial-streams"></a>

**If you want to stream part of a track, you can use the range request**

**`curl -v -o partial.mp4 -H "Range:bytes=81920-" "{url to aac stream}"`**

**You will need to calculate the number of bytes that you want to start and/or finish at**[  
](https://7digital.gitbook.io/api-doc/api-specifics)

