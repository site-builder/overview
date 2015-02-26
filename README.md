# Exploring Microservices

### Services:

public:
   * receiver:  accepts pings when deployments should be updated
   * registrar: api for creating and updating deployments
   * frontend:  web interface to registrar

private:
   * builder:   builds source
   * deployer:  deploys to target locations
   * fetcher:   retrieves most recent source
   * notifier:  notifies owners when events occur
   * operator:  http api that orchestrates communication between apps


### Workflows

When a deployment needs to be updated:

   receiver -> fetcher -> builder -> notifier

When a new deployment is created or updated:

   frontend -> registrar -> operator -> fetcher
                                     -> builder
                                     -> deployer
                                     -> notifier

When a deployment is ready to be updated:

   receiver -> operator -> fetcher
                        -> builder
                        -> deployer
                        -> notifier

### Diagram

![diagram](https://rawgithub.com/site-builder/overview/master/diagram.svg)
