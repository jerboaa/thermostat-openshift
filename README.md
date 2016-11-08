# Image Streams and Application Templates for Thermostat on OpenShift

## Thermostat Storage Template

In order to boot up a Thermostat Storage example the Thermostat image streams and the Thermostat Storage (Ephemeral) storage template need to get loaded into your project. This can be done via:

    $ oc create -f imagestreams-thermostat.json
    $ oc create -f thermostat-storage-template.json 
    $ oc process thermostat-storage-ephemeral | oc create -f -

