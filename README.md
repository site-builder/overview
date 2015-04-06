# Site Builder

All apps under the [site-builder](https://github.com/site-builder/) organization
are an experiment by [Sandro Padin](https://github.com/spadin) to build an
open-source microservices based app.

This is a learning exercise for me. Hopefully it can also help anyone interested
in learning how to implement an app using microservices.

### Services:

public:

* processor: accepts pings when deployments should be updated
* registrar: api for creating and updating deployments
* frontend:  web interface to registrar

private:

* builder:  builds source
* deployer: deploys to target locations
* fetcher:  retrieves most recent source
* notifier: notifies owners when events occur
* operator: http api that orchestrates communication between apps

queues:

* to-be-fetched: deployments that need to be fetched
* fetched: deployments that have been fetched
* to-be-built: deployments ready to be built
* built: deployments that have been built
* to-be-deployed: deployments ready to be deployed
* deployed: deployments that have been deployed
* to-be-notified: finished deployments can now notify owners
* notified: owners have been notified

### Workflows

When a deployment needs to be updated:

      processor -> fetcher -> builder -> notifier

When a new deployment is created or updated:

      frontend -> registrar -> operator -> fetcher
                                        -> builder
                                        -> deployer
                                        -> notifier

When a deployment is ready to be updated:

      processor -> operator -> fetcher
                            -> builder
                            -> deployer
                            -> notifier

### Diagram

![diagram](https://rawgithub.com/site-builder/overview/master/diagram.svg)
