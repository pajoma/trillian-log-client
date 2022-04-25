# trillian-log-client
Java gRPC stubs for calling the trillian log server api. 

See this [page](https://github.com/google/trillian) to learn about Google's Trillian project for tamper-proof logs. 

See the following quick example for using these stubs: 

````java
    LogLeaf leaf = LogLeaf.newBuilder()
        .setLeafValue(ByteString.copyFrom(leafValue))
        .setExtraData(ByteString.copyFrom(extraData))
        .build();

    QueueLeafRequest request = QueueLeafRequest.newBuilder()
        .setLeaf(leaf)
        .setLogId(logId)
        .build();

    QueueLeafResponse response;
        try {
            response = TrillianLogGrpc.newBlockingStub(this.channel).queueLeaf(request);
        } catch (Exception e) {
            log.atSevere().withCause(e).log("Failed to queue leaf");
            throw e;
        }
````