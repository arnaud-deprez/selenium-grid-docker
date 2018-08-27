# Selenium OpenShift Templates

This is based on the [official selenium grid images](https://github.com/SeleniumHQ/docker-selenium) but it's compatible with Openshift permission policy.

## Setup With Helm (recommended)

[Helm](https://docs.helm.sh) (aka The package manager for Kubernetes) is the recommended way to setup the `cicd` infrastructure and so `jenkins`.
To install `helm cli` and `tiller` on `Openshift`, please follow the guideline [here](https://github.com/arnaud-deprez/cicd-openshift/blob/master/README.md).

Once it is done, you can run the following: 

```sh
namespace=cicd
oc new-project $namespace
# install objects
helm upgrade -i --set ingress.enabled=true --set ingress.hostname="<ingress_hostname>" selenium charts/selenium
# trigger builds
oc start-build selenium-chrome-docker
oc start-build selenium-firefox-docker
```

For example, with `minishift` you can setup the hostname with:

```sh
namespace=cicd
oc new-project $namespace
helm upgrade -i --set ingress.enabled=true --set ingress.hostname=hub-cicd.$(minishift ip).nip.io selenium charts/selenium
# trigger builds
oc start-build selenium-chrome-docker
oc start-build selenium-firefox-docker
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
