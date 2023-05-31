# Lightstreamer - Chat-Tile Demo - Java Adapter #

<!-- START DESCRIPTION lightstreamer-example-chattile-adapter-java -->

The *Chat-Tile Demo* implements a simple chat/collaborative application based on [Lightstreamer](http://www.lightstreamer.com) for its real-time communication needs.

This project shows the Data Adapter and Metadata Adapters for the *Chat-Tile Demo* and how they can be plugged into Lightstreamer Server.

As an example of a client using this adapter, you may refer to the [Chat-Tile Demo - HTML (JQuery, Masonry) Client](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-client-javascript) and view the corresponding [Live Demo](http://demos.lightstreamer.com/ChatTileDemo/).

## Details

This project includes the implementation of the [SmartDataProvider](https://lightstreamer.com/api/ls-adapter-inprocess/latest/com/lightstreamer/interfaces/data/SmartDataProvider.html) interface and the [MetadataProviderAdapter](https://lightstreamer.com/api/ls-adapter-inprocess/latest/com/lightstreamer/interfaces/metadata/MetadataProviderAdapter.html) interface for the *Lightstreamer Chat-Tile Demo*. Please refer to [General Concepts](https://lightstreamer.com/docs/ls-server/latest/General%20Concepts.pdf) for more details about Lightstreamer Adapters.

### Java Data Adapter and MetaData Adapter

The Data Adapter accepts message submission for the unique chat room. The sender is identified by an IP address and a nickname.

The Metadata Adapter inherits from the reusable [LiteralBasedProvider](https://github.com/Lightstreamer/Lightstreamer-lib-adapter-java-inprocess#literalbasedprovider-metadata-adapter) and just adds a simple support for message submission. It should not be used as a reference for a real case of client-originated message handling, as no guaranteed delivery and no clustering support is shown.
<!-- END DESCRIPTION lightstreamer-example-chattile-adapter-java -->


### The Adapter Set Configuration

This Adapter Set is configured and will be referenced by the clients as `CHATTILE`. 

The `adapters.xml` file for the *Chat-Tile Demo*, should look like:

```xml      
<?xml version="1.0"?>
<adapters_conf id="CHATTILE">

    <metadata_adapter_initialised_first>Y</metadata_adapter_initialised_first>

    <metadata_provider>
        <adapter_class>com.lightstreamer.adapters.ChatTileDemo.ChatTileMetaAdapter</adapter_class>
  
        <!--
          TCP port on which Sun/Oracle's JMXMP connector will be
          listening.
        -->
        <param name="jmxPort">9999</param>
        
        <!-- configure the dedicated pool for notifyUserMessage call, see source code of ChatTileMetaAdapter -->
        <messages_pool>
            <max_pending_requests>100</max_pending_requests>
            <max_queue>100</max_queue>
        </messages_pool>
        
    </metadata_provider>
    
    <data_provider>
        <adapter_class>com.lightstreamer.adapters.ChatTileDemo.ChatTileAdapter</adapter_class>
          
    </data_provider>
</adapters_conf>
```

<i>NOTE: not all configuration options of an Adapter Set are exposed by the file suggested above. 
You can easily expand your configurations using the generic template, see the [Java In-Process Adapter Interface Project](https://github.com/Lightstreamer/Lightstreamer-lib-adapter-java-inprocess#configuration) for details.</i><br>
<br>
Please refer [here](https://lightstreamer.com/docs/ls-server/latest/General%20Concepts.pdf) for more details about Lightstreamer Adapters.

## Install
If you want to install a version of this demo in your local Lightstreamer Server, follow these steps:
* Download *Lightstreamer Server* (Lightstreamer Server comes with a free non-expiring demo license for 20 connected users) from [Lightstreamer Download page](http://www.lightstreamer.com/download.htm), and install it, as explained in the `GETTING_STARTED.TXT` file in the installation home directory.
* Get the `deploy.zip` file of the [latest release](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java/releases), unzip it, and copy the just unzipped `ChatTile` folder into the `adapters` folder of your Lightstreamer Server installation.
* [Optional] Customize the logging settings in log4j configuration file: `ChatTile/classes/log4j2.xml`.
* Launch Lightstreamer Server.
* Test the Adapter, launching the client listed in [Clients Using This Adapter](#clients-using-this-adapter).

## Build

To build your own version of `example-ChatTile-adapter-java-x.y.z-SNAPSHOT.jar` instead of using the one provided in the `deploy.zip` file from the [Install](#install) section above, you have two options:
either use [Maven](https://maven.apache.org/) (or other build tools) to take care of dependencies and building (recommended) or gather the necessary jars yourself and build it manually.
For the sake of simplicity only the Maven case is detailed here.

### Maven

You can easily build and run this application using Maven through the pom.xml file located in the root folder of this project. As an alternative, you can use an alternative build tool (e.g. Gradle, Ivy, etc.) by converting the provided pom.xml file.

Assuming Maven is installed and available in your path you can build the demo by running
```sh 
 mvn install dependency:copy-dependencies 
```

## See Also 

### Clients Using This Adapter
<!-- START RELATED_ENTRIES -->
<!-- END RELATED_ENTRIES -->

* [Lightstreamer - Chat-Tile Demo - JQuery Client](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-client-javascript)

<!-- END RELATED_ENTRIES -->

### Related Projects

* [Lightstreamer - Chat Demo - Java Adapter](https://github.com/Lightstreamer/Lightstreamer-example-Chat-adapter-java)
* [LiteralBasedProvider Metadata Adapter](https://github.com/Lightstreamer/Lightstreamer-lib-adapter-java-inprocess#literalbasedprovider-metadata-adapter)
* [Lightstreamer - Basic Messenger Demo - Java Adapter](https://github.com/Lightstreamer/Lightstreamer-example-Messenger-adapter-java)
* [Lightstreamer - Basic Messenger Demo - HTML Client](https://github.com/Lightstreamer/Lightstreamer-example-Messenger-client-javascript)

## Lightstreamer Compatibility Notes

- Compatible with Lightstreamer SDK for Java In-Process Adapters since version 8.0.
- For a version of this example compatible with Lightstreamer SDK for Java Adapters versions 7.3 to 7.4, please refer to [this tag](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java/tree/last_for_interface_7.4.x).
- For a version of this example compatible with Lightstreamer SDK for Java Adapters version 6.0, please refer to [this tag](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java/tree/pre_mvn).
- For a version of this example compatible with Lightstreamer SDK for Java Adapters version 5.1, please refer to [this tag](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java/tree/for_Lightstreamer_5.1).
