```yaml
# Configuration for Yandex Table (YT), a distributed storage and processing system.
yt:
  # Authentication token for YT. Replace 'YOUR TOKEN SECRET NAME' with the actual secret name for the YT token.
  token: 'YOUR TOKEN SECRET NAME'

# Configuration for Yandex Query Language (YQL), a query language for data processing.
yql:
  # Authentication token for YQL. Replace 'YOUR TOKEN SECRET NAME' with the actual secret name for the YQL token.
  token: 'YOUR TOKEN SECRET NAME'

# Configuration for SOY, likely a service or system used in the pipeline.
soy:
  # Authentication token for SOY. Replace 'YOUR TOKEN SECRET NAME' with the actual secret name for the SOY token.
  token: 'YOUR TOKEN SECRET NAME'

# Common configuration for the Alice VINS project.
alice_common:
  # OAuth token for Yandex Plus, used for authentication. This is a predefined token name for the Alice VINS robot.
  ya_plus_robot_token: robot-alice-vins_oauth_token

# Specifies the order in which acceptance tests should be run.
acceptance_order:
  # A list of groups of modules to run in order. Each group is a list of module keys.
  -
    # The first group contains a single module: 'check_analytics_info'.
    - check_analytics_info
```
