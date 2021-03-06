**NOTE** Analytics gathering has been removed from the Lumogon client, this page is preserved as a record of the old behaviour.

## [Obsolete] Anonymous Aggregate User Behaviour Analytics

Lumogon gathers anonymous aggregate user behaviour analytics and reports these to Google Analytics.

### Why?

The Lumogon team is interested in learning how users are using Lumogon to explore
their containers. This aggregate data helps us to prioritize issues and new features
based on how Lumogon is actually used.

We will also use the analytics to help monitor the health of the Lumogon reporting
service. If our analytics data suggests that more reports are uploaded than our
service receives, then this might be an indication that our service is not keeping
up with user demand.

### What?
Lumogon's analytics record some shared information for every event:

- The Google Analytics version, i.e. `1` (https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#v)
- The Lumogon analytics tracking ID, e.g. `UA-54263865-7` (https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#tid)
- A Docker analytics user ID, e.g. `7TRN:IPZB:QYBB:VPBQ:UMPP:KARE:6ZNR:XE6T:7EWV:PKF4:ZOJD:TPYS`. This is generated by `docker`. This does not allow us to track individual users but does enable us to accurately measure user counts vs. event counts (https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#cid)
- The Lumogon application name, e.g. `Lumogon` (https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#an)
- The Lumogon application version, e.g. `1.0.0` (https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#av)
- The Lumogon analytics hit type, e.g. `screenview` (https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#t)
- The Lumogon analytics screen view, e.g. `list` (https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#cd)

Lumogon's analytics records the following different events:

- a `screenview` hit type with the official Lumogon command you ran (with arguments stripped), e.g. `lumogon capabilities`
- an `event` type that indicates that an upload to the report viewer service was at least attempted

You can disable all analytics by passing `--disable-analytics` on the command line.

It is impossible for the Lumogon team to match any particular event to any particular user.

### When/Where?
Lumogon's analytics are sent during Lumogon's execution to Google Analytics over HTTPS.

### Who?

The anonymous aggregate data is accessible to the Lumogon team at Puppet, Inc.

### How?

The code is viewable in [analytics](https://github.com/puppetlabs/lumogon/blob/master/analytics/ga.go).
Analytics are processed in a separate background process and fail fast to avoid delaying any execution.
They will fail immediately and silently if you have no network connection.

### Opting out

Lumogon analytics help improve the quality and direction of the Lumogon project
and leaving analytics enabled is appreciated. However, if you want to opt out of
Lumogon's analytics, you can pass the following CLI argument at runtime:

```sh
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock puppet/lumogon --disable-analytics
```
