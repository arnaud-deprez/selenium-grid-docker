# Selenium OpenShift Templates [![Build Status](https://travis-ci.com/arnaud-deprez/selenium-grid-docker.svg?branch=master)](https://travis-ci.com/arnaud-deprez/selenium-grid-docker)

This is based on the [official selenium grid images](https://github.com/SeleniumHQ/docker-selenium) but it's compatible with Openshift permission policy.

## Setup With Helm (recommended)

[Helm](https://docs.helm.sh) (aka The package manager for Kubernetes) is the recommended way to setup the `cicd` infrastructure and so `jenkins`.
To install `helm cli` and `tiller` on `Openshift`, please follow the guideline [here](https://github.com/arnaud-deprez/cicd-openshift/blob/master/README.md).

Once it is done, you can run the following: 

```sh
namespace=cicd
oc new-project $namespace
# configure build
helm template --name selenium --set nameOverride=selenium charts/openshift-build | oc apply -f -
# trigger builds
oc start-build selenium-chrome-docker
oc start-build selenium-firefox-docker
# deploy
helm template --name selenium -f charts/openshift-build/values.yaml --set ingress.enabled=true --set ingress.hostname="<ingress_hostname>" charts/selenium | oc apply -f -
```

For example, with `minishift` you can setup the hostname with:

```sh
helm template --name selenium -f charts/openshift-build/values.yaml --set ingress.enabled=true --set ingress.hostname="hub-cicd.$(minishift ip).nip.io" charts/selenium | oc apply -f -
```

## Setup with openshift templates

```bash
oc process -f openshift/selenium-hub.yaml | oc apply -f -
oc process -f openshift/selenium-node-chrome.yaml | oc apply -f -
oc process -f openshift/selenium-node-firefox.yaml | oc apply -f -
```

## Example

![openshift 1 hub 1 node](http://i.imgur.com/Ux3VcE3.png)
![hub 1 node](http://i.imgur.com/FBIDvta.png)
![openshift 1 hub 1 nodes](http://i.imgur.com/JpMkwTP.png)
![hub 2 nodes](http://i.imgur.com/LBqQ0KS.png)
