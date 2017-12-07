# Kafka Connect to import/export data
## Configure custom consumer

Kafka Connect is a tool included with Kafka that imports and exports
data to Kafka. It is an extensible tool that runs connectors, which
implement the custom logic for interacting with an external system.
For example: A simple connectors that import data from a file to a
Kafka topic and export data from a Kafka topic to a file.

### For standalone mode (Windows)

1. Create source file and add data, so that it can be streamed line by line to the other file(sink).

2. Add source and sink file paths in the below properties files appropriately:

       notepad config/connect-file-source.properties
       notepad config/connect-file-sink.properties

    Note: First-time user fix directory paths in `config/connect-standalone.properties`

3. To run the Kafka connect:

       bin\windows\connect-standalone.bat  config\connect-standalone.properties config\connect-file-source.properties config\connect-file-sink.properties
