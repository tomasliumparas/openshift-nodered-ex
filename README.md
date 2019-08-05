
## Node-RED app on OpenShift
-----------------

This example will install Node-RED on OpenShift using S2I NodeJS strategy.


### Create a new Node-RED instance from template

```bash
oc new-app -f https://github.com/tomasliumparas/openshift-nodered-ex/blob/master/openshift/templates/nodered-persistent.yaml
```


### Environment variables

| Variable | Default value    | Description                 |
| -------- | ---------------- | --------------------------- |
| FLOWS    | /data/flows.json | Path to Node-RED flows file |

### Node-RED UI
