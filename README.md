# trillian-log-client
Java gRPC stubs for calling the trillian log server api. 

See this [page](https://github.com/google/trillian) to learn about Google's Trillian project for tamper-proof logs. 

## Example
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

## Accesing the maven repository

Generate a Github PAT and store it in your settings.xml

````xml
<settings>
    <servers>
        <server>
            <id>github</id>
            <username></username>
            <password>your generated token with package:read</password>
        </server>
    </servers>
</settings>

````

and add the repo to your pom.xml (or your settins.xml)

````xml

    <repositories>
        <repository>
            <id>github</id>
            <url>https://maven.pkg.github.com/pajoma/trillian-log-client</url>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
    </repositories>
````