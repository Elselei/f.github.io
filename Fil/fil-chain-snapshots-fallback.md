- 获取快照当天日期指向,x-amz-website-redirect-location字段为当天快照指向


```
curl -I https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_latest.car                                                   master untracked
HTTP/1.1 200 OK
x-amz-id-2: Jtfni2sXCBDaaAX0piqYmFB4It5ADWnFqoDRx65w6NRLYrZFYXlodWU5Y42V1ujjnE0CDRPhS+U=
x-amz-request-id: 304W3R9FWQ65XGTC
Date: Mon, 16 May 2022 14:18:30 GMT
Last-Modified: Mon, 16 May 2022 13:44:22 GMT
ETag: "f47a71a73f9cbffe1daa3a57617521b8-8912"
x-amz-website-redirect-location: https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_1813200_2022-05-16_12-00-00.car
Accept-Ranges: bytes
Content-Type: binary/octet-stream
Server: AmazonS3
Content-Length: 74751622475

```