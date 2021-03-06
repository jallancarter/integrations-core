# Agent Check: TokuMX

## Overview

This check collects TokuMX metrics like:

* Opcounters
* Replication lag
* Cache table utilization and storage size

And more.

## Setup
### Installation

The TokuMX check is packaged with the Agent, so simply [install the Agent](https://app.datadoghq.com/account/settings#agent) on your TokuMX servers. If you need the newest version of the check, install the `dd-check-tokumx` package.

### Configuration
#### Prepare TokuMX

In a Mongo shell, create a read-only user for the Datadog Agent in the `admin` database:

```
# Authenticate as the admin user.
use admin
db.auth("admin", "<YOUR_TOKUMX_ADMIN_PASSWORD>")
# Add a user for Datadog Agent
db.addUser("datadog", "<UNIQUEPASSWORD>", true)
```

#### Connect the Agent

Create a file `tokumx.yaml` in the Agent's `conf.d` directory:

```
init_config:

instances:
  - server: mongodb://datadog:<UNIQUEPASSWORD>@localhost:27017
```

Restart the Agent to start sending TokuMX metrics to Datadog.

### Validation

Run the Agent's `info` subcommand and look for `tokuxmx` under the Checks section:

```
  Checks
  ======
    [...]

    tokumx
    -------
      - instance #0 [OK]
      - Collected 26 metrics, 0 events & 1 service check

    [...]
```

## Compatibility

The tokumx check is compatible with all major platforms.

## Data Collected
### Metrics
See [metadata.csv](https://github.com/DataDog/integrations-core/blob/master/tokumx/metadata.csv) for a list of metrics provided by this check.

### Events
**Replication state changes**:

This check emits an event each time a TokuMX node has a change in its replication state.

### Service Checks

`tokumx.can_connect`:

Returns CRITICAL if the Agent cannot connect to TokuMX to collect metrics, otherwise OK.

## Troubleshooting

If you have any questions about Datadog or a use case our [Docs](https://docs.datadoghq.com/) didn’t mention, we’d love to help! Here’s how you can reach out to us:

### Visit the Knowledge Base

Learn more about what you can do in Datadog on the [Support Knowledge Base](https://datadog.zendesk.com/agent/).

### Web Support

Messages in the [event stream](https://app.datadoghq.com/event/stream) containing **@support-datadog** will reach our Support Team. This is a convenient channel for referencing graph snapshots or a particular event. In addition, we have a livechat service available during the day (EST) from any page within the app.

### By Email

You can also contact our Support Team via email at [support@datadoghq.com](mailto:support@datadoghq.com).

### Over Slack

Reach out to our team and other Datadog users on [Slack](http://chat.datadoghq.com/).

## Further Reading
To get a better idea of how (or why) to monitor TokuMX databases with Datadog, check out our [series of blog posts](https://www.datadoghq.com/blog/monitor-key-tokumx-metrics-mongodb-applications/) about it.
