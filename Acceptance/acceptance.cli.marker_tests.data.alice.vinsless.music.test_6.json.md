```json
[
    {  // Start of the JSON object
    "context": {  // Start of the context object, which provides additional information about the request
        "expected": {  // Expected response or behavior from the server
            "directives": "client_action:player_next_track",  // Specifies the action for the client (e.g., play the next track)
            "intent": "personal_assistant.scenarios.player_next_track"  // Indicates the intent of the request (play the next track)
        },
        "request": {  // Nested request object containing detailed information
            "app_preset": "quasar",  // Specifies the application preset being used
            "device_state": {  // Describes the current state of the device
                "alarm_state": {  // Information about the device's alarm state
                    "currently_playing": false,  // Indicates whether an alarm is currently playing
                    "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191025T070000Z\r\nDTEND:20191025T070000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191025T070000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"  // iCalendar data for scheduled alarms
                },
                "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191025T070000Z\r\nDTEND:20191025T070000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191025T070000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",  // Another iCalendar string for alarms state
                "device_config": {  // Configuration settings for the device
                    "content_settings": "medium",  // Specifies content settings (e.g., medium quality)
                    "spotter": "alisa"  // Indicates the voice assistant being used (e.g., Alisa)
                },
                "is_tv_plugged_in": false,  // Indicates whether a TV is connected to the device
                "last_watched": {  // Information about the last watched media
                    "movies": [],  // List of last watched movies (empty in this case)
                    "tv_shows": [],  // List of last watched TV shows (empty in this case)
                    "videos": []  // List of last watched videos (empty in this case)
                },
                "music": {  // Information about the current music state
                    "currently_playing": {  // Details about the currently playing track
                        "track_id": "45778945",  // Unique ID of the track
                        "track_info": {  // Metadata about the track
                            "albums": [  // List of albums associated with the track
                                {
                                    "artists": [  // List of artists associated with the album
                                        {
                                            "composer": false,  // Indicates if the artist is a composer
                                            "cover": {  // Cover image details for the artist
                                                "prefix": "cc8b2aa7.p.1006719/",  // Prefix for the cover image URL
                                                "type": "from-artist-photos",  // Type of cover image
                                                "uri": "avatars.yandex.net/get-music-content/117546/cc8b2aa7.p.1006719/%%"  // URI for the cover image
                                            },
                                            "genres": [],  // List of genres associated with the artist (empty in this case)
                                            "id": 1006719,  // Unique ID of the artist
                                            "name": "HUGEL",  // Name of the artist
                                            "various": false  // Indicates if the artist is a compilation
                                        },
                                        {
                                            "composer": false,  // Indicates if the artist is a composer
                                            "cover": {  // Cover image details for the artist
                                                "prefix": "e924194e.a.8044362-1",  // Prefix for the cover image URL
                                                "type": "from-album-cover",  // Type of cover image
                                                "uri": "avatars.yandex.net/get-music-content/149669/e924194e.a.8044362-1/%%"  // URI for the cover image
                                            },
                                            "genres": [],  // List of genres associated with the artist (empty in this case)
                                            "id": 5696005,  // Unique ID of the artist
                                            "name": "Amber van Day",  // Name of the artist
                                            "various": false  // Indicates if the artist is a compilation
                                        }
                                    ],
                                    "available": true,  // Indicates if the album is available
                                    "availableForMobile": true,  // Indicates if the album is available on mobile
                                    "availableForPremiumUsers": true,  // Indicates if the album is available for premium users
                                    "availablePartially": false,  // Indicates if the album is partially available
                                    "bests": [],  // List of best tracks in the album (empty in this case)
                                    "buy": [],  // List of purchase options (empty in this case)
                                    "contentWarning": "explicit",  // Indicates if the album has explicit content
                                    "coverUri": "avatars.yandex.net/get-music-content/139444/be710d02.a.6151649-1/%%",  // URI for the album cover
                                    "genre": "dance",  // Genre of the album
                                    "id": 6151649,  // Unique ID of the album
                                    "labels": [  // List of labels associated with the album
                                        {
                                            "id": 159,  // Unique ID of the label
                                            "name": "Warner"  // Name of the label
                                        }
                                    ],
                                    "ogImage": "avatars.yandex.net/get-music-content/139444/be710d02.a.6151649-1/%%",  // Open Graph image for the album
                                    "recent": false,  // Indicates if the album is recent
                                    "releaseDate": "2018-11-30T00:00:00+03:00",  // Release date of the album
                                    "title": "WTF",  // Title of the album
                                    "trackCount": 1,  // Number of tracks in the album
                                    "trackPosition": {  // Position of the current track in the album
                                        "index": 1,  // Index of the track
                                        "volume": 1  // Volume number of the track
                                    },
                                    "type": "single",  // Type of the album (e.g., single)
                                    "veryImportant": false,  // Indicates if the album is very important
                                    "year": 2018  // Year of the album's release
                                }
                            ],
                            "artists": [  // List of artists associated with the track
                                {
                                    "composer": false,  // Indicates if the artist is a composer
                                    "cover": {  // Cover image details for the artist
                                        "prefix": "cc8b2aa7.p.1006719/",  // Prefix for the cover image URL
                                        "type": "from-artist-photos",  // Type of cover image
                                        "uri": "avatars.yandex.net/get-music-content/117546/cc8b2aa7.p.1006719/%%"  // URI for the cover image
                                    },
                                    "genres": [],  // List of genres associated with the artist (empty in this case)
                                    "id": 1006719,  // Unique ID of the artist
                                    "name": "HUGEL",  // Name of the artist
                                    "various": false  // Indicates if the artist is a compilation
                                },
                                {
                                    "composer": false,  // Indicates if the artist is a composer
                                    "cover": {  // Cover image details for the artist
                                        "prefix": "e924194e.a.8044362-1",  // Prefix for the cover image URL
                                        "type": "from-album-cover",  // Type of cover image
                                        "uri": "avatars.yandex.net/get-music-content/149669/e924194e.a.8044362-1/%%"  // URI for the cover image
                                    },
                                    "genres": [],  // List of genres associated with the artist (empty in this case)
                                    "id": 5696005,  // Unique ID of the artist
                                    "name": "Amber van Day",  // Name of the artist
                                    "various": false  // Indicates if the artist is a compilation
                                }
                            ],
                            "available": true,  // Indicates if the track is available
                            "availableForPremiumUsers": true,  // Indicates if the track is available for premium users
                            "availableFullWithoutPermission": false,  // Indicates if the track is fully available without permission
                            "batchId": "sync-43fa408f-8107-4124-bec5-de4a1fb10f37",  // Batch ID for synchronization
                            "batchInfo": {  // Information about the batch
                                "index": 0,  // Index of the batch
                                "rid": "4a4ba5e5-dfdb-48ce-8346-32cc26731005",  // Unique ID for the batch
                                "type": "onDemand"  // Type of the batch (e.g., on-demand)
                            },
                            "contentWarning": "explicit",  // Indicates if the track has explicit content
                            "coverUri": "avatars.yandex.net/get-music-content/139444/be710d02.a.6151649-1/%%",  // URI for the track cover
                            "durationMs": 160730,  // Duration of the track in milliseconds
                            "fileSize": 3858180,  // File size of the track in bytes
                            "id": "45778945",  // Unique ID of the track
                            "lyricsAvailable": true,  // Indicates if lyrics are available for the track
                            "major": {  // Major information about the track
                                "id": 4,  // Unique ID of the major
                                "name": "WARNER"  // Name of the major
                            },
                            "normalization": {  // Normalization settings for the track
                                "gain": -8.91,  // Gain value for normalization
                                "peak": 32766  // Peak value for normalization
                            },
                            "ogImage": "avatars.yandex.net/get-music-content/139444/be710d02.a.6151649-1/%%",  // Open Graph image for the track
                            "previewDurationMs": 30000,  // Duration of the track preview in milliseconds
                            "realId": "45778945",  // Real ID of the track
                            "rememberPosition": false,  // Indicates if the track position should be remembered
                            "storageDir": "369919_8d8b1df0.68296619.1.45778945",  // Storage directory for the track
                            "title": "WTF",  // Title of the track
                            "type": "music"  // Type of the track (e.g., music)
                        }
                    },
                    "player": {  // Information about the music player
                        "pause": false  // Indicates if the player is paused
                    },
                    "playlist_owner": "",  // Owner of the playlist (empty in this case)
                    "session_id": "e5nCe26j"  // Unique session ID for the music player
                },
                "sound_level": 2,  // Current sound level of the device
                "sound_muted": false,  // Indicates if the sound is muted
                "timers": {  // Information about active timers
                    "active_timers": []  // List of active timers (empty in this case)
                },
                "video": {  // Information about the current video state
                    "current_screen": "music_player"  // Indicates the current screen being displayed (e.g., music player)
                }
            },
            "experiments": {},  // Placeholder for experimental features (empty in this case)
            "fetcher_mode": "voice",  // Indicates the mode of fetching data (e.g., voice)
            "request_id": "ffffffff-ffff-ffff-4acd-fbfac4b4f936",  // Unique ID for the request
            "session_id": "ffffffff-ffff-ffff-4acd-fbfac4b4f936__ffffffff-ffff-ffff-6905-c2e5b083ef85",  // Unique ID for the session
            "session_sequence": 0,  // Sequence number of the session
            "text": "следующая песня",  // Text of the user's request (e.g., "next song")
            "vins_intent": "personal_assistant\tscenarios\tplayer_next_track"  // Intent of the request as interpreted by the VINS system
            "voice_base64_binary": "T2dnUwACAAAAAAAAAADcEx1PAAAAAIyt9ZcBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAANwTHU8BAAAAwxy3XgP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAEALAAAAAAAA\n3BMdTwIAAACmvq02AyMtKkgAscwo5SWQLtKlE1H32gZwZMcuAhy7rJceXts46cnXlQhWSA8nS05L\n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\n"
            // Specifies the base64-encoded binary representation of the voice input.
        }
    },
    {
    "request": {  // Start of the request object
        "expected": {  // Expected response or behavior from the server
            "directives": "client_action:audio_play, server_action:@@mm_stack_engine_get_next",  // Specifies actions for the client and server (e.g., play audio and get the next item)
            "intent": "personal_assistant.scenarios.music_play"  // Indicates the intent of the request (music playback)
        },
        "request": {  // Nested request object containing detailed information
            "app_preset": "quasar",  // Specifies the application preset being used
            "device_state": {  // Describes the current state of the device
                "alarm_state": {  // Information about the device's alarm state
                    "currently_playing": false,  // Indicates whether an alarm is currently playing
                    "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191025T070000Z\r\nDTEND:20191025T070000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191025T070000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"  // iCalendar data for scheduled alarms
                },
                "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191025T070000Z\r\nDTEND:20191025T070000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191025T070000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",  // Another iCalendar string for alarms state
                "device_config": {  // Configuration settings for the device
                    "content_settings": "medium",  // Specifies content settings (e.g., medium quality)
                    "spotter": "alisa"  // Indicates the voice assistant being used (e.g., Alisa)
                },
                "is_tv_plugged_in": false,  // Indicates whether a TV is connected to the device
                "last_watched": {  // Information about the last watched media
                    "movies": [],  // List of last watched movies (empty in this case)
                    "tv_shows": [],  // List of last watched TV shows (empty in this case)
                    "videos": []  // List of last watched videos (empty in this case)
                },
                "music": {  // Information about the current music state
                    "currently_playing": {  // Details about the currently playing track
                        "track_id": "59364874",  // Unique ID of the track
                        "track_info": {  // Metadata about the track
                            "albums": [  // List of albums associated with the track
                                {
                                    "artists": [  // List of artists associated with the album
                                        {
                                            "composer": false,  // Indicates if the artist is a composer
                                            "cover": {  // Cover image details for the artist
                                                "prefix": "87e7a4e5.a.7686704-1",  // Prefix for the cover image URL
                                                "type": "from-album-cover",  // Type of cover image
                                                "uri": "avatars.yandex.net/get-music-content/103235/87e7a4e5.a.7686704-1/%%"  // URI for the cover image
                                            },
                                            "genres": [],  // List of genres associated with the artist (empty in this case)
                                            "id": 1033565,  // Unique ID of the artist
                                            "name": "Alok",  // Name of the artist
                                            "various": false  // Indicates if the artist is a compilation
                                        },
                                        {
                                            "composer": false,  // Indicates if the artist is a composer
                                            "cover": {  // Cover image details for the artist
                                                "prefix": "cc8b2aa7.p.1006719/",  // Prefix for the cover image URL
                                                "type": "from-artist-photos",  // Type of cover image
                                                "uri": "avatars.yandex.net/get-music-content/117546/cc8b2aa7.p.1006719/%%"  // URI for the cover image
                                            },
                                            "genres": [],  // List of genres associated with the artist (empty in this case)
                                            "id": 1006719,  // Unique ID of the artist
                                            "name": "HUGEL",  // Name of the artist
                                            "various": false  // Indicates if the artist is a compilation
                                        },
                                        {
                                            "composer": false,  // Indicates if the artist is a composer
                                            "cover": {  // Cover image details for the artist
                                                "prefix": "e924194e.a.8044362-1",  // Prefix for the cover image URL
                                                "type": "from-album-cover",  // Type of cover image
                                                "uri": "avatars.yandex.net/get-music-content/149669/e924194e.a.8044362-1/%%"  // URI for the cover image
                                            },
                                            "genres": [],  // List of genres associated with the artist (empty in this case)
                                            "id": 5696005,  // Unique ID of the artist
                                            "name": "Amber van Day",  // Name of the artist
                                            "various": false  // Indicates if the artist is a compilation
                                        }
                                    ],
                                    "available": true,  // Indicates if the album is available
                                    "availableForMobile": true,  // Indicates if the album is available on mobile
                                    "availableForPremiumUsers": true,  // Indicates if the album is available for premium users
                                    "availablePartially": false,  // Indicates if the album is partially available
                                    "bests": [],  // List of best tracks in the album (empty in this case)
                                    "buy": [],  // List of purchase options (empty in this case)
                                    "coverUri": "avatars.yandex.net/get-music-content/2266607/d52be455.a.9091805-1/%%",  // URI for the album cover
                                    "genre": "dance",  // Genre of the album
                                    "id": 9091805,  // Unique ID of the album
                                    "labels": [  // List of labels associated with the album
                                        {
                                            "id": 1725055,  // Unique ID of the label
                                            "name": "CONTROVERSIA"  // Name of the label
                                        }
                                    ],
                                    "ogImage": "avatars.yandex.net/get-music-content/2266607/d52be455.a.9091805-1/%%",  // Open Graph image for the album
                                    "recent": false,  // Indicates if the album is recent
                                    "releaseDate": "2019-11-01T00:00:00+03:00",  // Release date of the album
                                    "title": "I Don't Wanna Talk",  // Title of the album
                                    "trackCount": 1,  // Number of tracks in the album
                                    "trackPosition": {  // Position of the current track in the album
                                        "index": 1,  // Index of the track
                                        "volume": 1  // Volume number of the track
                                    },
                                    "type": "single",  // Type of the album (e.g., single)
                                    "veryImportant": false,  // Indicates if the album is very important
                                    "year": 2019  // Year of the album's release
                                }
                            ],
                            "artists": [  // List of artists associated with the track
                                {
                                    "composer": false,  // Indicates if the artist is a composer
                                    "cover": {  // Cover image details for the artist
                                        "prefix": "87e7a4e5.a.7686704-1",  // Prefix for the cover image URL
                                        "type": "from-album-cover",  // Type of cover image
                                        "uri": "avatars.yandex.net/get-music-content/103235/87e7a4e5.a.7686704-1/%%"  // URI for the cover image
                                    },
                                    "genres": [],  // List of genres associated with the artist (empty in this case)
                                    "id": 1033565,  // Unique ID of the artist
                                    "name": "Alok",  // Name of the artist
                                    "various": false  // Indicates if the artist is a compilation
                                },
                                {
                                    "composer": false,  // Indicates if the artist is a composer
                                    "cover": {  // Cover image details for the artist
                                        "prefix": "cc8b2aa7.p.1006719/",  // Prefix for the cover image URL
                                        "type": "from-artist-photos",  // Type of cover image
                                        "uri": "avatars.yandex.net/get-music-content/117546/cc8b2aa7.p.1006719/%%"  // URI for the cover image
                                    },
                                    "genres": [],  // List of genres associated with the artist (empty in this case)
                                    "id": 1006719,  // Unique ID of the artist
                                    "name": "HUGEL",  // Name of the artist
                                    "various": false  // Indicates if the artist is a compilation
                                },
                                {
                                    "composer": false,  // Indicates if the artist is a composer
                                    "cover": {  // Cover image details for the artist
                                        "prefix": "e924194e.a.8044362-1",  // Prefix for the cover image URL
                                        "type": "from-album-cover",  // Type of cover image
                                        "uri": "avatars.yandex.net/get-music-content/149669/e924194e.a.8044362-1/%%"  // URI for the cover image
                                    },
                                    "genres": [],  // List of genres associated with the artist (empty in this case)
                                    "id": 5696005,  // Unique ID of the artist
                                    "name": "Amber van Day",  // Name of the artist
                                    "various": false  // Indicates if the artist is a compilation
                                }
                            ],
                            "available": true,  // Indicates if the track is available
                            "availableForPremiumUsers": true,  // Indicates if the track is available for premium users
                            "availableFullWithoutPermission": false,  // Indicates if the track is fully available without permission
                            "batchId": "sync-72794314-02c6-41d5-9532-b05fcdc91457",  // Batch ID for synchronization
                            "batchInfo": {  // Information about the batch
                                "index": 1,  // Index of the batch
                                "rid": "4a4ba5e5-dfdb-48ce-8346-32cc26731005",  // Unique ID for the batch
                                "type": "onDemand"  // Type of the batch (e.g., on-demand)
                            },
                            "coverUri": "avatars.yandex.net/get-music-content/2266607/d52be455.a.9091805-1/%%",  // URI for the track cover
                            "durationMs": 144040,  // Duration of the track in milliseconds
                            "fileSize": 3457566,  // File size of the track in bytes
                            "id": "59364874",  // Unique ID of the track
                            "lyricsAvailable": true,  // Indicates if lyrics are available for the track
                            "major": {  // Major information about the track
                                "id": 4,  // Unique ID of the major
                                "name": "WARNER"  // Name of the major
                            },
                            "normalization": {  // Normalization settings for the track
                                "gain": -8.55,  // Gain value for normalization
                                "peak": 32766  // Peak value for normalization
                            },
                            "ogImage": "avatars.yandex.net/get-music-content/2266607/d52be455.a.9091805-1/%%",  // Open Graph image for the track
                            "previewDurationMs": 30000,  // Duration of the track preview in milliseconds
                            "realId": "59364874",  // Real ID of the track
                            "rememberPosition": false,  // Indicates if the track position should be remembered
                            "storageDir": "1652671_3519f7c4.88118271.2.59364874",  // Storage directory for the track
                            "title": "I Don't Wanna Talk",  // Title of the track
                            "type": "music"  // Type of the track (e.g., music)
                        }
                    },
                    "player": {  // Information about the music player
                        "pause": false  // Indicates if the player is paused
                    },
                    "playlist_owner": "",  // Owner of the playlist (empty in this case)
                    "session_id": "e5nCe26j"  // Unique session ID for the music player
                },
                "sound_level": 2,  // Current sound level of the device
                "sound_muted": false,  // Indicates if the sound is muted
                "timers": {  // Information about active timers
                    "active_timers": []  // List of active timers (empty in this case)
                },
                "video": {  // Information about the current video state
                    "current_screen": "music_player"  // Indicates the current screen being displayed (e.g., music player)
                }
            },
            "experiments": {},  // Placeholder for experimental features (empty in this case)
            "fetcher_mode": "voice",  // Indicates the mode of fetching data (e.g., voice)
            "request_id": "ffffffff-ffff-ffff-6905-c2e5b083ef85",  // Unique ID for the request
            "session_id": "ffffffff-ffff-ffff-4acd-fbfac4b4f936__ffffffff-ffff-ffff-6905-c2e5b083ef85",  // Unique ID for the session
            "session_sequence": 1,  // Sequence number of the session
            "text": "включи спокойную музыку",  // Text of the user's request (e.g., "play calm music")
            "vins_intent": "personal_assistant\tscenarios\tvinsless\tmusic"  // Intent of the request as interpreted by the VINS system
            "voice_base64_binary": "T2dnUwACAAAAAAAAAACINM1rAAAAAB8RcRwBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAIg0zWsBAAAA7G2hZwP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAEALAAAAAAAA\niDTNawIAAADfXrcVAx0pKkgArxrMq0m6WQaaWEkKVOpLfh6/+5j8xOrnSnE4SAxPK6sWJqSIiOVo\n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\n"
            // Specifies the base64-encoded binary representation of the voice input.
        }
    }
}
}
]
```
