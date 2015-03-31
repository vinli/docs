Overview
========

The Vinli Android SDKs utilize the excellent [RxJava library](https://github.com/ReactiveX/RxJava) to provide a reactive interface through which apps may access both the physical Vinli Device and the Vinli Web APIs. Following reactive principles allows the Vinli SDKs to gracefully clear the asynchronous hurdles inherent in bluetooth device communication. For a lengthier explaination of the benefits of reactive APIs, [Couchbase has a great blog post](http://blog.couchbase.com/why-couchbase-chose-rxjava-new-java-sdk).

The Vinli Android SDK is split into two pieces, Net and Direct. The Net SDK provides access to the backend APIs--including authentication, device information, and diagnostic services. The Direct SDK provides direct access to Vinli Basic devices. Through the Direct SDK, apps can discover Vinli devices, query device information, and observe realtime vehicle telemetry.
