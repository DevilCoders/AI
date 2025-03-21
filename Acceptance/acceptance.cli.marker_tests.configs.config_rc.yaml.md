```yaml
nirvana:  
    # The `nirvana` block contains configuration settings related to Nirvana workflows.

    quota:  
    # Specifies the quota for Nirvana workflow execution.  
    # This field is currently empty and should be populated with the appropriate quota value.

    hitman_guid:  
    # Specifies the GUID of the Nirvana workflow (Hitman).  
    # This field is currently empty and should be populated with the appropriate GUID.

yt:  
    # The `yt` block contains configuration settings related to YT (Yandex.Tank or Yandex Table).

    token: robot-voice-qa_yt_token  
    # Specifies the YT token for authentication.  
    # The token is associated with the `robot-voice-qa` account.

    proxy: hahn  
    # Specifies the YT proxy URL as `hahn`.  
    # This is the cluster where YT operations will be executed.

    pool:  
    # Specifies the YT pool for resource allocation.  
    # This field is currently empty and should be populated with the appropriate pool name.

    mr_account: alice-dev  
    # Specifies the MapReduce (MR) quota account as `alice-dev`.  
    # This account is used for MR operations.

    mr_output_ttl: 1  
    # Specifies the time-to-live (TTL) for MR output data as 1 (likely in days).

    mr_output_path: 'home[#if param["mr-account"] != meta.owner]/${param["mr-account"]}[/#if]/${meta.owner}/nirvana/marker_tests/${meta.operation_uid}'  
    # Specifies the output path for MR results.  
    # The path is dynamically constructed using template logic.  
    # It includes placeholders for the MR account, owner, and operation UID.

yql:  
    # The `yql` block contains configuration settings related to YQL (Yandex Query Language).

    token: robot-voice-qa_yql_token  
    # Specifies the YQL token for authentication.  
    # The token is associated with the `robot-voice-qa` account.

arcanum:  
    # The `arcanum` block contains configuration settings related to Arcanum (a code review tool).

    token: robot-voice-qa_arcanum_token  
    # Specifies the Arcanum token for authentication.  
    # The token is associated with the `robot-voice-qa` account.

soy:  
    # The `soy` block contains configuration settings related to SOY (likely a custom service or tool).

    token: robot-voice-qa-soy-token  
    # Specifies the SOY token for authentication.  
    # The token is associated with the `robot-voice-qa` account.

alice:  
    # The `alice` block contains configuration settings related to the Alice voice assistant.

    uniproxy_url: 'wss://uniproxy.alice.yandex.net/uni.ws'  
    # Specifies the URL for the uniproxy service.  
    # This is used for communication with the Alice voice assistant.

    vins_url: 'http://megamind-rc.alice.yandex.net/speechkit/app/pa/'  
    # Specifies the URL for the Vins (Voice INterface Service) or Megamind service.  
    # This is used for speech processing and natural language understanding.

    oauth: bass_testing_analyst_token  
    # Specifies the OAuth token for authentication.  
    # The token is associated with the `bass_testing_analyst` account.

    scraper_timeout: '12h'  
    # Specifies the timeout for the scraper as `12h` (12 hours).  
    # This determines how long the scraper will wait before timing out.

    scraper_pool: alice  
    # Specifies the pool for the scraper as `alice`.  
    # This determines the resource pool for scraper operations.

    asr_chunk_size: -1  
    # Specifies the chunk size for ASR (Automatic Speech Recognition) as `-1`.  
    # A value of `-1` typically indicates no size limit.

    experiments:  
    # Specifies additional experiments or configuration options.  
    # This field is currently empty and can be populated as needed.
```
