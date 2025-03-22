```yaml
# Configuration for Yandex Table (YT), a distributed storage and processing system.
yt:
  # Authentication token for YT. Must be overridden with a valid token.
  token: 'OVERRIDE THIS'
  # Specifies the YT proxy to use (e.g., 'hahn' for the Hahn cluster).
  proxy: hahn
  # MapReduce account to use for YT operations.
  mr_account: alice-dev

# Configuration for Yandex Query Language (YQL), a query language for data processing.
yql:
  # Authentication token for YQL. Must be overridden with a valid token.
  token: 'OVERRIDE THIS'

# Configuration for Sandbox, a system for managing resources and artifacts.
sandbox:
  # Owner of the Sandbox resources (e.g., 'VINS').
  owner: VINS
  # Authentication token for Sandbox. Must be overridden with a valid token.
  token: 'OVERRIDE THIS'

# Configuration for SOY, likely a service or system used in the pipeline.
soy:
  # Authentication token for SOY. Must be overridden with a valid token.
  token: 'OVERRIDE THIS'

# Configuration for Nirvana, a workflow automation system.
nirvana:
  # Quota for Nirvana jobs (e.g., 'voice-core').
  quota: voice-core
  # Name of the Nirvana project (e.g., 'alice_vins').
  project: alice_vins
  # Label for Nirvana jobs (e.g., 'acceptance').
  label: acceptance

# Common configuration for the Alice VINS project.
alice_common:
  # Path to the table storing dialog logs in YT. The '%(date)s' placeholder is dynamically replaced with a date.
  dialog_logs_table: '//home/voice/vins/logs/dialogs/%(date)s'
  # Path to the table storing session data in YT. The '%(date)s' placeholder is dynamically replaced with a date.
  sessions_table: '//home/voice/dialog/sessions/%(date)s'
  # OAuth token for Yandex Plus, used for authentication.
  ya_plus_robot_token: robot-alice-vins_oauth_token
  # Specifies the scraper pool for YT (e.g., 'alice').
  scraper_over_yt_pool: alice
  # Token for Arcanum, a code review system, used for authentication.
  arcanum_robot_token: robot-voice-qa_arcanum_token

# Specifies the order in which acceptance tests should be run.
acceptance_order:
  # Currently empty, but can be populated with module keys (e.g., 'check_analytics_info').
  -
    - ''

# Configuration for the 'check_analytics_info' module, which validates analytics data.
check_analytics_info:
  # Path to the input table in YT for analytics checks.
  input_table: '//home/alice/toloka/accept/ue2e_quasar/basket'
  # URL for preparing VINS states (e.g., for speechkit).
  vins_url_state_preparer: 'http://vins.hamster.alice.yandex.net/speechkit/app/pa/'
  # WebSocket URL for Uniproxy, a service for handling requests.
  uniproxy_url: 'wss://beta.uniproxy.alice.yandex.net/alice-uniproxy-hamster/uni.ws'
  # URL for the test version of VINS.
  test_vins_url: 'http://megamind-rc.alice.yandex.net/speechkit/app/pa/'
  # URL for the stable version of VINS.
  stable_vins_url: 'http://vins.hamster.alice.yandex.net/speechkit/app/pa/'
  # List of experiments to enable (e.g., 'analytics_info=1').
  experiments: ['analytics_info=1', 'tunneller_analytics_info=1']
  # Arcadia revision number for the check (e.g., 7183819).
  revision: 7183819
```
