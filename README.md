
## Node-RED app on OpenShift
-----------------
This example will install Node-RED on OpenShift using S2I NodeJS strategy.


### Quick start

Create all needed resources using template:
```bash
oc new-app -f https://raw.githubusercontent.com/tomasliumparas/openshift-nodered-ex/master/openshift/templates/nodered-persistent.yaml
```

Example output:
```bash
--> Deploying template "it-test/nodered-persistent" for "https://raw.githubusercontent.com/tomasliumparas/openshift-nodered-ex/master/openshift/templates/nodered-persistent.yaml" to project it-test

     Node-RED S2I (Persistent)
     ---------
     Node-RED is a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways.

     The following service(s) have been created in your project:
     nodered-example

     For more information about using this template, including OpenShift considerations, see https://github.com/tomasliumparas/openshift-nodered-ex/blob/master/README.md

     * With parameters:
        * Name=nodered-example
        * Namespace=openshift
        * Version of NodeJS Image=8
        * Memory Limit=512Mi
        * Volume Capacity=1Gi
        * Git Repository URL=https://github.com/tomasliumparas/openshift-nodered-ex.git
        * Git Reference=
        * Context Directory=
        * Disable SCM SSL verification=true
        * Application Hostname=
        * GitHub Webhook Secret=xbVIek8J5BOAWkPQjXvKKSRVpRcjKE6pW1TIe68f # generated
        * Generic Webhook Secret=fTFakCQ2RFnAyy0qKOPcF0rAPjE2g0RORdBCqS5E # generated
        * Custom NPM Mirror URL=

--> Creating resources ...
    service "nodered-example" created
    route "nodered-example" created
    imagestream "nodered-example" created
    buildconfig "nodered-example" created
    deploymentconfig "nodered-example" created
    persistentvolumeclaim "nodered-example-data" created
    configmap "nodered-example-config" created
--> Success
    Access your application via route 'nodered-example-it-test.paas.dpd.lt'
    Build scheduled, use 'oc logs -f bc/nodered-example' to track its progress.
    Run 'oc status' to view your app.
```


### Environment variables

| Variable | Default value    | Description                 |
| -------- | ---------------- | --------------------------- |
| FLOWS    | /data/flows.json | Path to Node-RED flows file |

### Node-RED UI

Node-RED ui is accessible via created route. In the above example that would be:
```bash
--> Success
    Access your application via route 'nodered-example-it-test.paas.dpd.lt'
```

Default login credentials are:
```bash
User: admin
Password: adminadminadmin
```

Changing login credentials:
```bash
# Get a Node-RED pod
oc get pods

# Open pod's terminal session
oc rsh <pod>

#Generate password hash using Node-RED admin utility
node-red-admin hash-pw

# Edit Node-RED config map and place the generated password hash
oc edit configmap nodered-example-config
```
