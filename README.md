# HFR to Tanzania Health Supply Chain Mediator


[![Java CI Badge](https://github.com/SoftmedTanzania/thscp-mediator-hfr/workflows/Java%20CI%20with%20Maven/badge.svg)](https://github.com/SoftmedTanzania/thscp-mediator-hfr/actions?query=workflow%3A%22Java+CI+with+Maven%22)
[![Coverage Status](https://coveralls.io/repos/github/SoftmedTanzania/thscp-mediator-hfr/badge.svg?branch=development)](https://coveralls.io/github/SoftmedTanzania/thscp-mediator-hfr?branch=development)

An [OpenHIM](http://openhim.org/) mediator for handling system integration between HFR and Tanzania Health Supply Chain Mediator.

## 1. Dev Requirements

1. Java 1.8
2. IntelliJ or Visual Studio Code
3. Maven 3.6.3

## 2. Mediator Configuration

This mediator is designed to work with HFR that send JSON Payloads while communicating with the THSCP via the HIM.

### 3 Configuration Parameters

The configuration parameters specific to the mediator and destination system can be found at

`src/main/resources/mediator.properties`

```
    # Mediator Properties
    mediator.name=THSCP-Mediator-HFR
    mediator.host=localhost
    mediator.port=3022
    mediator.timeout=60000
    mediator.heartbeats=true
    
    core.host=localhost
    core.api.port=8080
    core.api.user=openhim-username
    core.api.password=openhim-password

    
    destination.host=destination-system-address
    destination.api.port=destination-system-address-port
    destination.api.path=/destination-system-path
    destination.scheme=destination-system-scheme
```

The configuration parameters specific to the mediator and the mediator's metadata can be found at

`src/main/resources/mediator-registration-info.json`

```
    {
      "urn": "urn:uuid:cc763b80-86e7-11eb-a6ca-ab6591b1bfac",
      "version": "0.1.0",
      "name": "THSCP-Mediator-HFR",
      "description": "An OpenHIM mediator for handling system integrations between HFR and THSCP",
      "endpoints": [
        {
          "name": "THSCP-Mediator-HFR Route",
          "host": "localhost",
          "port": "3022",
          "path": "/thscp",
          "type": "http"
        }
      ],
      "defaultChannelConfig": [
        {
          "name": "THSCP-Mediator-HFR",
          "urlPattern": "^/thscp$",
          "type": "http",
          "allow": ["thscp-mediator-hfr"],
          "routes": [
            {
              "name": "THSCP-Mediator-HFR Route",
              "host": "localhost",
              "port": "3022",
              "path": "/thscp",
              "type": "http",
              "primary": "true"
            }
          ]
        }
      ]
    }
```

## 4. Deployment

To build and run the mediator after performing the above configurations, run the following

```
  mvn clean package -DskipTests=true -e source:jar javadoc:jar
  java -jar target/thscp-mediator-hfr-<version>-jar-with-dependencies.jar
```
