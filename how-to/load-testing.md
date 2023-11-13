---
title: How to set up a load test
---
# {{page.title}}

## Load Testing - Best Practices

* Generate **seed data** to help identify database bottlenecks
* Set up **ramp-up periods** and **pauses** to generate incremental load and emulate users' think time
* Use **distinct user accounts** to avoid contention over session data retrieval
* Monitor **queued requests** to pinpoint infrastructure limits
* Design your tests to be **idempotent** in order to compare results

## Test Plan Templates

* Login/Logout
* Screen Preparation (Navigate)
* Submit Request
* Submit Request(AJAX)
* REST/SOAP service call

## Test Plan Composition

* Thread groups
* Configurations
* Assertions
* Extractors
* Samplers
* Listeners

## Result Analiysis

* JMeter Output
* Service Center Logs
* Performance Counters

### Forge components

* Performance csi
* Infrastructure Monitor

## Additional Considerations

* **JavaScript code** won't be executed by JMeter
* Adjust number of **concurrent threads** to the hardware resources running JMeter
* Isolate test script **custom data** using request defaults, user variables and CSV data sets
* Use **parameters** to instantiate variables via **command line**
* Use "View Results" listeners when **fine-tuning** test scripts

* [ ] todo continue video at 15:30 m

## References

* [How to setup a load test in 5 minutes]
* [JMeter]

[How to setup a load test in 5 minutes]: https://learn.outsystems.com/training/journeys/tester-654/how-to-set-up-a-load-test-in-5-minutes/o11/2467
[JMeter]: https://jmeter.apache.org/