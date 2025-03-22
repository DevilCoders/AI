```json
[
    // Start of an array containing JSON objects
    {
        // Start of the first JSON object
        "context": {
            // "context" key holds metadata or contextual information
            "expected": {
                // "expected" key defines what the system anticipates as a response
                "directives": "",
                // "directives" key: Specifies actions the client should perform (empty means no specific actions)
                "intent": "personal_assistant.scenarios.alarm_cancel"
                // "intent" key: Specifies the intent of the request (e.g., canceling an alarm)
            },
            "request": {
                // "request" key holds details about the user's request
                "app_preset": "quasar",
                // "app_preset" key: Specifies the application or platform being used (e.g., Quasar)
                "device_state": {
                    // "device_state" key: Holds the current state of the device
                    "alarm_state": {
                        // "alarm_state" key: Contains details about the alarm state
                        "currently_playing": false,
                        // "currently_playing" key: Indicates whether an alarm is currently playing (false means no)
                        "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191104T023000Z\r\nDTEND:20191104T023000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191104T023000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"
                        // "icalendar" key: Contains iCalendar data for the alarm (e.g., start time, trigger, and action)
                    },
                    "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191104T023000Z\r\nDTEND:20191104T023000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191104T023000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",
                    // "alarms_state" key: Contains iCalendar data for all alarms (similar to "icalendar")
                    "device_config": {
                        // "device_config" key: Contains configuration settings for the device
                        "content_settings": "without",
                        // "content_settings" key: Specifies content settings (e.g., "without" meaning no specific settings)
                        "spotter": "alisa"
                        // "spotter" key: Specifies the voice assistant being used (e.g., Alisa)
                    },
                    "is_tv_plugged_in": false,
                    // "is_tv_plugged_in" key: Indicates whether a TV is plugged in (false means no)
                    "last_watched": {
                        // "last_watched" key: Contains information about the last watched media
                        "movies": [],
                        // "movies" key: Empty array, meaning no movies were recently watched
                        "tv_shows": [],
                        // "tv_shows" key: Empty array, meaning no TV shows were recently watched
                        "videos": []
                        // "videos" key: Empty array, meaning no videos were recently watched
                    },
                    "music": {
                        // "music" key: Contains information about the current music state
                        "currently_playing": {
                            // "currently_playing" key: Contains details about the currently playing track
                            "track_id": "58240667",
                            // "track_id" key: Unique identifier for the track
                            "track_info": {
                                // "track_info" key: Contains metadata about the track
                                "albums": [
                                    // "albums" key: Array of albums associated with the track
                                    {
                                        // Start of an album object
                                        "artists": [
                                            // "artists" key: Array of artists associated with the album
                                            {
                                                // Start of an artist object
                                                "composer": false,
                                                // "composer" key: Indicates whether the artist is a composer (false means no)
                                                "cover": {
                                                    // "cover" key: Contains cover art details for the artist
                                                    "prefix": "73eda69a.a.8816774-1",
                                                    // "prefix" key: URL prefix for the cover art
                                                    "type": "from-album-cover",
                                                    // "type" key: Specifies the type of cover art (e.g., from album cover)
                                                    "uri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%"
                                                    // "uri" key: Full URL for the cover art
                                                },
                                                "genres": [],
                                                // "genres" key: Empty array, meaning no specific genres are associated
                                                "id": 4200895,
                                                // "id" key: Unique identifier for the artist
                                                "name": "SHAED",
                                                // "name" key: Name of the artist
                                                "various": false
                                                // "various" key: Indicates whether the artist is a "various artists" placeholder (false means no)
                                            },
                                            {
                                                // Start of another artist object
                                                "composer": false,
                                                "cover": {
                                                    "prefix": "fc57b98d.p.4153286/",
                                                    "type": "from-artist-photos",
                                                    "uri": "avatars.yandex.net/get-music-content/143117/fc57b98d.p.4153286/%%"
                                                },
                                                "genres": [],
                                                "id": 4153286,
                                                "name": "ZAYN",
                                                "various": false
                                            }
                                        ],
                                        "available": true,
                                        // "available" key: Indicates whether the album is available (true means yes)
                                        "availableForMobile": true,
                                        // "availableForMobile" key: Indicates whether the album is available on mobile (true means yes)
                                        "availableForPremiumUsers": true,
                                        // "availableForPremiumUsers" key: Indicates whether the album is available for premium users (true means yes)
                                        "availablePartially": false,
                                        // "availablePartially" key: Indicates whether the album is partially available (false means no)
                                        "bests": [],
                                        // "bests" key: Empty array, meaning no tracks are marked as best in the album
                                        "buy": [],
                                        // "buy" key: Empty array, meaning no purchase options are available
                                        "coverUri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                        // "coverUri" key: URL for the album cover art
                                        "genre": "pop",
                                        // "genre" key: Specifies the genre of the album (e.g., pop)
                                        "id": 8816774,
                                        // "id" key: Unique identifier for the album
                                        "labels": [
                                            // "labels" key: Array of record labels associated with the album
                                            {
                                                "id": 445884,
                                                // "id" key: Unique identifier for the label
                                                "name": "Photo Finish"
                                                // "name" key: Name of the label
                                            }
                                        ],
                                        "ogImage": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                        // "ogImage" key: URL for the Open Graph image (used for social media sharing)
                                        "recent": false,
                                        // "recent" key: Indicates whether the album is recent (false means no)
                                        "releaseDate": "2019-09-26T00:00:00+03:00",
                                        // "releaseDate" key: Specifies the release date of the album
                                        "title": "Trampoline",
                                        // "title" key: Title of the album
                                        "trackCount": 1,
                                        // "trackCount" key: Total number of tracks in the album
                                        "trackPosition": {
                                            // "trackPosition" key: Specifies the position of the track in the album
                                            "index": 1,
                                            // "index" key: Index of the track in the album
                                            "volume": 1
                                            // "volume" key: Volume number (e.g., 1 for a single-disc album)
                                        },
                                        "type": "single",
                                        // "type" key: Specifies the type of album (e.g., single)
                                        "veryImportant": false,
                                        // "veryImportant" key: Indicates whether the album is marked as very important (false means no)
                                        "year": 2019
                                        // "year" key: Release year of the album
                                    }
                                ],
                                "artists": [
                                    // "artists" key: Array of artists associated with the track
                                    {
                                        // Start of an artist object (same structure as above)
                                        "composer": false,
                                        "cover": {
                                            "prefix": "73eda69a.a.8816774-1",
                                            "type": "from-album-cover",
                                            "uri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%"
                                        },
                                        "genres": [],
                                        "id": 4200895,
                                        "name": "SHAED",
                                        "various": false
                                    },
                                    {
                                        // Start of another artist object
                                        "composer": false,
                                        "cover": {
                                            "prefix": "fc57b98d.p.4153286/",
                                            "type": "from-artist-photos",
                                            "uri": "avatars.yandex.net/get-music-content/143117/fc57b98d.p.4153286/%%"
                                        },
                                        "genres": [],
                                        "id": 4153286,
                                        "name": "ZAYN",
                                        "various": false
                                    }
                                ],
                                "available": true,
                                // "available" key: Indicates whether the track is available (true means yes)
                                "availableForPremiumUsers": true,
                                // "availableForPremiumUsers" key: Indicates whether the track is available for premium users (true means yes)
                                "availableFullWithoutPermission": false,
                                // "availableFullWithoutPermission" key: Indicates whether the track is fully available without permission (false means no)
                                "batchId": "sync-5b72cdb2-04e7-4b64-ad13-77b9fe509614",
                                // "batchId" key: Unique identifier for the batch (e.g., for synchronization)
                                "batchInfo": {
                                    // "batchInfo" key: Contains metadata about the batch
                                    "index": 0,
                                    // "index" key: Index of the batch
                                    "rid": "086ebe4e-aa04-4bee-a6ca-3493868d76a5",
                                    // "rid" key: Unique identifier for the request
                                    "type": "onDemand"
                                    // "type" key: Specifies the type of batch (e.g., on-demand)
                                },
                                "coverUri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                // "coverUri" key: URL for the track cover art
                                "durationMs": 184320,
                                // "durationMs" key: Duration of the track in milliseconds
                                "fileSize": 4424306,
                                // "fileSize" key: Size of the track file in bytes
                                "id": "58240667",
                                // "id" key: Unique identifier for the track
                                "lyricsAvailable": true,
                                // "lyricsAvailable" key: Indicates whether lyrics are available for the track (true means yes)
                                "major": {
                                    // "major" key: Contains details about the major label
                                    "id": 1,
                                    // "id" key: Unique identifier for the major label
                                    "name": "UNIVERSAL_MUSIC"
                                    // "name" key: Name of the major label
                                },
                                "normalization": {
                                    // "normalization" key: Contains audio normalization details
                                    "gain": -9.86,
                                    // "gain" key: Specifies the gain level for normalization
                                    "peak": 32766
                                    // "peak" key: Specifies the peak level for normalization
                                },
                                "ogImage": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                // "ogImage" key: URL for the Open Graph image (used for social media sharing)
                                "previewDurationMs": 30000,
                                // "previewDurationMs" key: Duration of the track preview in milliseconds
                                "realId": "58240667",
                                // "realId" key: Real identifier for the track
                                "rememberPosition": false,
                                // "rememberPosition" key: Indicates whether the playback position should be remembered (false means no)
                                "storageDir": "1031985_01e130c0.86503056.1.58240667",
                                // "storageDir" key: Specifies the storage directory for the track
                                "title": "Trampoline",
                                // "title" key: Title of the track
                                "type": "music"
                                // "type" key: Specifies the type of media (e.g., music)
                            }
                        },
                        "player": {
                            // "player" key: Contains details about the music player
                            "pause": true,
                            // "pause" key: Indicates whether the player is paused (true means yes)
                            "timestamp": 1572794442
                            // "timestamp" key: Timestamp of the player's state
                        },
                        "playlist_owner": "",
                        // "playlist_owner" key: Specifies the owner of the playlist (empty means no owner)
                        "session_id": "tfIMJ0J8"
                        // "session_id" key: Unique identifier for the music session
                    },
                    "sound_level": 5,
                    // "sound_level" key: Specifies the current sound level (e.g., 5 out of 10)
                    "sound_muted": false,
                    // "sound_muted" key: Indicates whether the sound is muted (false means no)
                    "timers": {
                        // "timers" key: Contains details about active timers
                        "active_timers": []
                        // "active_timers" key: Empty array, meaning no active timers
                    },
                    "video": {
                        // "video" key: Contains details about the video state
                        "current_screen": "main"
                        // "current_screen" key: Specifies the current screen being displayed (e.g., main screen)
                    }
                },
                "experiments": {},
                // "experiments" key: Empty object, meaning no experiments are active
                "fetcher_mode": "voice",
                // "fetcher_mode" key: Specifies the mode of fetching data (e.g., voice)
                "request_id": "ffffffff-ffff-ffff-2fb8-9a24a7664f43",
                // "request_id" key: Unique identifier for the request
                "session_id": "ffffffff-ffff-ffff-2fb8-9a24a7664f43__ffffffff-ffff-ffff-55c5-0c1b23ce0d62",
                // "session_id" key: Unique identifier for the session
                "session_sequence": 0,
                // "session_sequence" key: Sequence number for the session (0 means initial session)
                "text": "удали будильник",
                // "text" key: Contains the user's input text (e.g., "delete the alarm")
                "vins_intent": "personal_assistant\tscenarios\talarm_cancel"
                // "vins_intent" key: Specifies the intent of the request (e.g., canceling an alarm)
                "voice_base64_binary": "T2dnUwACAAAAAAAAAABrdEIrAAAAAOby4bkBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAGt0QisBAAAANh4sAAP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAMADAAAAAAAA\na3RCKwIAAAAYlKbGAS5IDKB3Fe8VpFG3tJtYXtmSCAm7mEZnxKGi27+DtOtApcETwCv/lCWdGRx2\n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\nrRZOa13gp6sIbz8=\n"
                // Specifies the base64-encoded binary representation of the voice input.
            }
        },
        "request": {
            // Second "request" key, possibly representing a nested or alternative request structure
            "expected": {
                // "expected" key defines what the system anticipates as a response
                "directives": "client_action:alarms_update, client_action:tts_play_placeholder",
                // "directives" key: Specifies actions the client should perform (e.g., update alarms, play text-to-speech placeholder)
                "intent": "personal_assistant.scenarios.alarm_set"
                // "intent" key: Specifies the intent of the request (e.g., setting an alarm)
            },
            "request": {
                // Nested "request" key, holding details about the user's request
                "app_preset": "quasar",
                // "app_preset" key: Specifies the application or platform being used (e.g., Quasar)
                "device_state": {
                    // "device_state" key: Holds the current state of the device
                    "alarm_state": {
                        // "alarm_state" key: Contains details about the alarm state
                        "currently_playing": false,
                        // "currently_playing" key: Indicates whether an alarm is currently playing (false means no)
                        "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nEND:VCALENDAR\r\n"
                        // "icalendar" key: Contains iCalendar data for the alarm (empty means no active alarms)
                    },
                    "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nEND:VCALENDAR\r\n",
                    // "alarms_state" key: Contains iCalendar data for all alarms (empty means no active alarms)
                    "device_config": {
                        // "device_config" key: Contains configuration settings for the device
                        "content_settings": "without",
                        // "content_settings" key: Specifies content settings (e.g., "without" meaning no specific settings)
                        "spotter": "alisa"
                        // "spotter" key: Specifies the voice assistant being used (e.g., Alisa)
                    },
                    "is_tv_plugged_in": false,
                    // "is_tv_plugged_in" key: Indicates whether a TV is plugged in (false means no)
                    "last_watched": {
                        // "last_watched" key: Contains information about the last watched media
                        "movies": [],
                        // "movies" key: Empty array, meaning no movies were recently watched
                        "tv_shows": [],
                        // "tv_shows" key: Empty array, meaning no TV shows were recently watched
                        "videos": []
                        // "videos" key: Empty array, meaning no videos were recently watched
                    },
                    "music": {
                        // "music" key: Contains information about the current music state
                        "currently_playing": {
                            // "currently_playing" key: Contains details about the currently playing track
                            "track_id": "58240667",
                            // "track_id" key: Unique identifier for the track
                            "track_info": {
                                // "track_info" key: Contains metadata about the track (same structure as above)
                                "albums": [
                                    {
                                        "artists": [
                                            {
                                                "composer": false,
                                                "cover": {
                                                    "prefix": "73eda69a.a.8816774-1",
                                                    "type": "from-album-cover",
                                                    "uri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%"
                                                },
                                                "genres": [],
                                                "id": 4200895,
                                                "name": "SHAED",
                                                "various": false
                                            },
                                            {
                                                "composer": false,
                                                "cover": {
                                                    "prefix": "fc57b98d.p.4153286/",
                                                    "type": "from-artist-photos",
                                                    "uri": "avatars.yandex.net/get-music-content/143117/fc57b98d.p.4153286/%%"
                                                },
                                                "genres": [],
                                                "id": 4153286,
                                                "name": "ZAYN",
                                                "various": false
                                            }
                                        ],
                                        "available": true,
                                        "availableForMobile": true,
                                        "availableForPremiumUsers": true,
                                        "availablePartially": false,
                                        "bests": [],
                                        "buy": [],
                                        "coverUri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                        "genre": "pop",
                                        "id": 8816774,
                                        "labels": [
                                            {
                                                "id": 445884,
                                                "name": "Photo Finish"
                                            }
                                        ],
                                        "ogImage": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                        "recent": false,
                                        "releaseDate": "2019-09-26T00:00:00+03:00",
                                        "title": "Trampoline",
                                        "trackCount": 1,
                                        "trackPosition": {
                                            "index": 1,
                                            "volume": 1
                                        },
                                        "type": "single",
                                        "veryImportant": false,
                                        "year": 2019
                                    }
                                ],
                                "artists": [
                                    {
                                        "composer": false,
                                        "cover": {
                                            "prefix": "73eda69a.a.8816774-1",
                                            "type": "from-album-cover",
                                            "uri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%"
                                        },
                                        "genres": [],
                                        "id": 4200895,
                                        "name": "SHAED",
                                        "various": false
                                    },
                                    {
                                        "composer": false,
                                        "cover": {
                                            "prefix": "fc57b98d.p.4153286/",
                                            "type": "from-artist-photos",
                                            "uri": "avatars.yandex.net/get-music-content/143117/fc57b98d.p.4153286/%%"
                                        },
                                        "genres": [],
                                        "id": 4153286,
                                        "name": "ZAYN",
                                        "various": false
                                    }
                                ],
                                "available": true,
                                "availableForPremiumUsers": true,
                                "availableFullWithoutPermission": false,
                                "batchId": "sync-5b72cdb2-04e7-4b64-ad13-77b9fe509614",
                                "batchInfo": {
                                    "index": 0,
                                    "rid": "086ebe4e-aa04-4bee-a6ca-3493868d76a5",
                                    "type": "onDemand"
                                },
                                "coverUri": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                "durationMs": 184320,
                                "fileSize": 4424306,
                                "id": "58240667",
                                "lyricsAvailable": true,
                                "major": {
                                    "id": 1,
                                    "name": "UNIVERSAL_MUSIC"
                                },
                                "normalization": {
                                    "gain": -9.86,
                                    "peak": 32766
                                },
                                "ogImage": "avatars.yandex.net/get-music-content/119639/73eda69a.a.8816774-1/%%",
                                "previewDurationMs": 30000,
                                "realId": "58240667",
                                "rememberPosition": false,
                                "storageDir": "1031985_01e130c0.86503056.1.58240667",
                                "title": "Trampoline",
                                "type": "music"
                            }
                        },
                        "player": {
                            "pause": true,
                            "timestamp": 1572794442
                        },
                        "playlist_owner": "",
                        "session_id": "tfIMJ0J8"
                    },
                    "sound_level": 5,
                    "sound_muted": false,
                    "timers": {
                        "active_timers": []
                    },
                    "video": {
                        "current_screen": "main"
                    }
                },
                "experiments": {},
                // "experiments" key: Empty object, meaning no experiments are active
                "fetcher_mode": "voice",
                // "fetcher_mode" key: Specifies the mode of fetching data (e.g., voice)
                "request_id": "ffffffff-ffff-ffff-55c5-0c1b23ce0d62",
                // "request_id" key: Unique identifier for the request
                "session_id": "ffffffff-ffff-ffff-2fb8-9a24a7664f43__ffffffff-ffff-ffff-55c5-0c1b23ce0d62",
                // "session_id" key: Unique identifier for the session
                "session_sequence": 1,
                // "session_sequence" key: Sequence number for the session (1 means second session)
                "text": "поставь будильник на семь тридцать",
                // "text" key: Contains the user's input text (e.g., "set an alarm for 7:30")
                "vins_intent": "personal_assistant\tscenarios\talarm_set"
                // "vins_intent" key: Specifies the intent of the request (e.g., setting an alarm)
                "voice_base64_binary": "T2dnUwACAAAAAAAAAAAPNlgjAAAAAEhJud4BE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAA82WCMBAAAAOrE0aQP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAEALAAAAAAAA\nDzZYIwIAAABMtXnRAyYyKkgB04U6aa7O9bQpz5XZG+ACyVKz2FiGr/EZQ03ieQhESaQbIYGASBRN\n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\n"
                // Specifies the base64-encoded binary representation of the voice input.
            }
        }
    }
    // End of the first JSON object
]
// End of the array
```
