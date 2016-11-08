# Image Streams and Application Templates for Thermostat on OpenShift

## Thermostat Storage Template

In order to boot up a Thermostat Storage example the Thermostat image streams and the Thermostat Storage (Ephemeral) storage template need to get loaded into your project. This can be done via:

    $ oc create -f imagestreams-thermostat.json
    $ oc create -f thermostat-storage-template.json 

Finally, an example Thermostat Storage deployment can be created by using default values with:

    $ oc process thermostat-storage-ephemeral | oc create -f -

Generated Thermostat agent credentials which can be used to log into the Thermostat Storage instance can get looked up with:

    $ oc env --list dc/thermostat-storage-ex | grep THERMOSTAT_AGENT
    THERMOSTAT_AGENT_USERNAME=thagentEIYI
    THERMOSTAT_AGENT_PASSWORD=X2KTQJGH

Similarly, Thermostat client credentials can get looked up with:

    $ oc env --list dc/thermostat-storage-ex | grep THERMOSTAT_CLIENT

Alternatively, credentials can get set ahead of time on template instantiation:

    $ oc process thermostat-storage-ephemeral \
          -v TH_AGENT_USERNAME=agent-tester \
          -v TH_AGENT_PASSWORD=agent-secrit \
          -v TH_CLIENT_USERNAME=client-tester \
          -v TH_CLIENT_PASSWORD=client-secrit \
          -v DATABASE_SERVICE_NAME=th-mongodb \
      | oc create -f -
