# Selenium OpenShift Templates

> OpenShift Templates used for a Scalable Selenium infrastructure

## Usage

```bash
oc process -f selenium-hub.yaml -p VERSION=3.11 | oc apply -f -
oc process -f selenium-node-chrome.yaml -p VERSION=3.11 | oc apply -f -
oc process -f selenium-node-firefox.yaml -p VERSION=3.11 | oc apply -f -
```

## Example

![openshift 1 hub 1 node](http://i.imgur.com/Ux3VcE3.png)
![hub 1 node](http://i.imgur.com/FBIDvta.png)
![openshift 1 hub 1 nodes](http://i.imgur.com/JpMkwTP.png)
![hub 2 nodes](http://i.imgur.com/LBqQ0KS.png)
