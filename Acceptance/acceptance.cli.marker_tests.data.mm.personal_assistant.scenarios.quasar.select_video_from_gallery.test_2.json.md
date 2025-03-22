```json
[  // Start of an array containing one or more request objects
    {  // Start of the first (and only) object in the array
        "context": {  // Start of the context object, which provides additional information about the request
            "expected": {  // Expected response or behavior from the server
                "directives": "client_action:show_gallery",  // Specifies the action for the client (e.g., show a gallery)
                "intent": "mm.personal_assistant.scenarios.video_play",  // Indicates the intent of the request (video playback)
                "xfail": true  // Indicates if the request is expected to fail (e.g., for testing purposes)
            },
            "request": {  // Nested request object containing detailed information
                "app_preset": "quasar",  // Specifies the application preset being used
                "device_state": {  // Describes the current state of the device
                    "alarm_state": {  // Information about the device's alarm state
                        "currently_playing": false,  // Indicates whether an alarm is currently playing
                        "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190507T143000Z\r\nDTEND:20190507T143000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190507T143000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T043000Z\r\nDTEND:20190512T043000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T043000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T040000Z\r\nDTEND:20190512T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190518T030000Z\r\nDTEND:20190518T030000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190518T030000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190519T040000Z\r\nDTEND:20190519T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190519T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190525T040000Z\r\nDTEND:20190525T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190525T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190526T040000Z\r\nDTEND:20190526T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190526T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190630T083000Z\r\nDTEND:20190630T083000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190630T083000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190829T160000Z\r\nDTEND:20190829T160000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190829T160000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190913T141000Z\r\nDTEND:20190913T141000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190913T141000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20191013T140000Z\r\nDTEND:20191013T140000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191013T140000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"  // iCalendar data for scheduled alarms
                    },
                    "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190507T143000Z\r\nDTEND:20190507T143000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190507T143000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T043000Z\r\nDTEND:20190512T043000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T043000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T040000Z\r\nDTEND:20190512T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190518T030000Z\r\nDTEND:20190518T030000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190518T030000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190519T040000Z\r\nDTEND:20190519T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190519T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190525T040000Z\r\nDTEND:20190525T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190525T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190526T040000Z\r\nDTEND:20190526T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190526T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190630T083000Z\r\nDTEND:20190630T083000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190630T083000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190829T160000Z\r\nDTEND:20190829T160000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190829T160000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190913T141000Z\r\nDTEND:20190913T141000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190913T141000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20191013T140000Z\r\nDTEND:20191013T140000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191013T140000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",  // Another iCalendar string for alarms state
                    "device_config": {  // Configuration settings for the device
                        "content_settings": "medium",  // Specifies content settings (e.g., medium quality)
                        "spotter": "alisa"  // Indicates the voice assistant being used (e.g., Alisa)
                    },
                    "is_tv_plugged_in": true,  // Indicates whether a TV is connected to the device
                    "last_watched": {  // Information about the last watched media
                        "movies": [],  // List of last watched movies (empty in this case)
                        "tv_shows": [],  // List of last watched TV shows (empty in this case)
                        "videos": [  // List of last watched videos
                            {
                                "play_uri": "https://yastatic.net/video-player/0x0fd98704a3/pages-common/ok/ok.html#html=%3Ciframe%20src%3D%22//ok.ru/videoembed/9542763926%3Fautoplay%3D1%26amp;ya%3D1%22%20frameborder%3D%220%22%20scrolling%3D%22no%22%20allowfullscreen%3D%221%22%20allow%3D%22autoplay;%20fullscreen;%20accelerometer;%20gyroscope;%20picture-in-picture%22%20aria-label%3D%22Video%22%3E%3C/iframe%3E&autoplay=yes&tv=1&clean=true",  // URI for playing the video
                                "progress": {  // Information about the playback progress
                                    "duration": 1227,  // Total duration of the video in seconds
                                    "played": 492  // Duration of the video that has been played in seconds
                                },
                                "provider_item_id": "http://ok.ru/video/9542763926",  // Unique ID of the video from the provider
                                "provider_name": "yavideo",  // Name of the video provider (e.g., Yandex Video)
                                "timestamp": 1572614838  // Timestamp of when the video was last watched
                            },
                            {
                                "play_uri": "youtube://blUGu9fZ3hA",  // URI for playing the video (YouTube)
                                "progress": {  // Information about the playback progress
                                    "duration": 5569,  // Total duration of the video in seconds
                                    "played": 2145  // Duration of the video that has been played in seconds
                                },
                                "provider_item_id": "blUGu9fZ3hA",  // Unique ID of the video from the provider (YouTube video ID)
                                "provider_name": "youtube",  // Name of the video provider (e.g., YouTube)
                                "timestamp": 1572623140  // Timestamp of when the video was last watched
                            }
                        ]
                    },
                    "music": {  // Information about the current music state
                        "currently_playing": {  // Details about the currently playing track
                            "track_id": "45466301",  // Unique ID of the track
                            "track_info": {  // Metadata about the track
                                "albums": [  // List of albums associated with the track
                                    {
                                        "artists": [  // List of artists associated with the album
                                            {
                                                "composer": false,  // Indicates if the artist is a composer
                                                "cover": {  // Cover image details for the artist
                                                    "prefix": "0519833a.a.6103411-1",  // Prefix for the cover image URL
                                                    "type": "from-album-cover",  // Type of cover image
                                                    "uri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%"  // URI for the cover image
                                                },
                                                "genres": [],  // List of genres associated with the artist (empty in this case)
                                                "id": 5908164,  // Unique ID of the artist
                                                "name": "Черный Рояль Самурая",  // Name of the artist
                                                "various": false  // Indicates if the artist is a compilation
                                            }
                                        ],
                                        "available": true,  // Indicates if the album is available
                                        "availableForMobile": true,  // Indicates if the album is available on mobile
                                        "availableForPremiumUsers": true,  // Indicates if the album is available for premium users
                                        "availablePartially": false,  // Indicates if the album is partially available
                                        "bests": [  // List of best tracks in the album
                                            45466306,
                                            45466301,
                                            45466302
                                        ],
                                        "buy": [],  // List of purchase options (empty in this case)
                                        "coverUri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // URI for the album cover
                                        "genre": "newage",  // Genre of the album
                                        "id": 6103411,  // Unique ID of the album
                                        "labels": [  // List of labels associated with the album
                                            {
                                                "id": 1250450,  // Unique ID of the label
                                                "name": "Black Piano Classic"  // Name of the label
                                            }
                                        ],
                                        "ogImage": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // Open Graph image for the album
                                        "recent": false,  // Indicates if the album is recent
                                        "title": "Звуки фортепьяно под звуки природы и леса",  // Title of the album
                                        "trackCount": 11,  // Number of tracks in the album
                                        "trackPosition": {  // Position of the current track in the album
                                            "index": 1,  // Index of the track
                                            "volume": 1  // Volume number of the track
                                        },
                                        "version": "Original Mix",  // Version of the album (e.g., Original Mix)
                                        "veryImportant": false,  // Indicates if the album is very important
                                        "year": 2019  // Year of the album's release
                                    }
                                ],
                                "artists": [  // List of artists associated with the track
                                    {
                                        "composer": false,  // Indicates if the artist is a composer
                                        "cover": {  // Cover image details for the artist
                                            "prefix": "0519833a.a.6103411-1",  // Prefix for the cover image URL
                                            "type": "from-album-cover",  // Type of cover image
                                            "uri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%"  // URI for the cover image
                                        },
                                        "genres": [],  // List of genres associated with the artist (empty in this case)
                                        "id": 5908164,  // Unique ID of the artist
                                        "name": "Черный Рояль Самурая",  // Name of the artist
                                        "various": false  // Indicates if the artist is a compilation
                                    }
                                ],
                                "available": true,  // Indicates if the track is available
                                "availableForPremiumUsers": true,  // Indicates if the track is available for premium users
                                "availableFullWithoutPermission": false,  // Indicates if the track is fully available without permission
                                "batchId": "sync-93f5db4f-b710-4796-9098-f17f60c920c2",  // Batch ID for synchronization
                                "batchInfo": {  // Information about the batch
                                    "index": 0,  // Index of the batch
                                    "rid": "1572614598593874-1501879132-megamind-sas-34-vins",  // Unique ID for the batch
                                    "type": "onDemand"  // Type of the batch (e.g., on-demand)
                                },
                                "coverUri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // URI for the track cover
                                "durationMs": 107000,  // Duration of the track in milliseconds
                                "fileSize": 2569195,  // File size of the track in bytes
                                "id": "45466301",  // Unique ID of the track
                                "lyricsAvailable": false,  // Indicates if lyrics are available for the track
                                "major": {  // Major information about the track
                                    "id": 134,  // Unique ID of the major
                                    "name": "ELECTRONIC_MUSIC_DISTRIBUTION"  // Name of the major
                                },
                                "normalization": {  // Normalization settings for the track
                                    "gain": -8.07,  // Gain value for normalization
                                    "peak": 32393  // Peak value for normalization
                                },
                                "ogImage": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // Open Graph image for the track
                                "previewDurationMs": 30000,  // Duration of the track preview in milliseconds
                                "realId": "45466301",  // Real ID of the track
                                "rememberPosition": false,  // Indicates if the track position should be remembered
                                "storageDir": "1445069_81617160.67748721.1.45466301",  // Storage directory for the track
                                "title": "Фортепьяно и звуки леса №1",  // Title of the track
                                "type": "music",  // Type of the track (e.g., music)
                                "version": "Original Mix"  // Version of the track (e.g., Original Mix)
                            }
                        },
                        "player": {  // Information about the music player
                            "pause": true,  // Indicates if the player is paused
                            "timestamp": 1572614604  // Timestamp of when the player state was last updated
                        },
                        "playlist_owner": "",  // Owner of the playlist (empty in this case)
                        "session_id": "tRJSHcPj"  // Unique session ID for the music player
                    },
                    "sound_level": 5,  // Current sound level of the device
                    "sound_muted": false,  // Indicates if the sound is muted
                    "timers": {  // Information about active timers
                        "active_timers": []  // List of active timers (empty in this case)
                    },
                    "video": {  // Information about the current video state
                        "current_screen": "gallery",  // Indicates the current screen being displayed (e.g., gallery)
                        "screen_state": {  // State of the current screen
                            "debug_info": {  // Debug information for the screen
                                "url": "/video/search?assistant=1&family=moderate&g=1.dg.20.1.-1&gta=qproxy&json_dump=searchdata&noredirect=1&rearr=forced_player_device%3Dquasar&rearr=scheme_Local/VideoSnippets/ReplaceVhDups%3D0&rearr=forced_qproxy_player%3D1&text=3+%D0%BA%D0%BE%D1%82%D0%B0",  // URL for the video search
                                "ya_video_request": "3 кота"  // Text of the video search request (e.g., "3 кота")
                            },
                            "items": [  // List of items in the gallery
                                {
                                    "available": 1,  // Indicates if the video is available
                                    "duration": 3865,  // Duration of the video in seconds
                                    "name": "Три кота - Сборник зимних серий",  // Name of the video
                                    "normalized_name": "3 кота - сборник зимних серий",  // Normalized name of the video
                                    "play_uri": "youtube://-E0JW1ONGPQ",  // URI for playing the video (YouTube)
                                    "price_from": 0,  // Price of the video (free in this case)
                                    "provider_info": [  // Information about the video provider
                                        {
                                            "available": 1,  // Indicates if the video is available
                                            "provider_item_id": "-E0JW1ONGPQ",  // Unique ID of the video from the provider
                                            "provider_name": "youtube",  // Name of the video provider (e.g., YouTube)
                                            "type": "video"  // Type of the content (e.g., video)
                                        }
                                    ],
                                    "provider_item_id": "-E0JW1ONGPQ",  // Unique ID of the video from the provider
                                    "provider_name": "youtube",  // Name of the video provider (e.g., YouTube)
                                    "source_host": "www.youtube.com",  // Host of the video source (e.g., YouTube)
                                    "thumbnail_url_16x9": "https://avatars.mds.yandex.net/get-vthumb/228771/e45fc9725cf00fa1b6fd00cb32224e60/800x360",  // URL for the video thumbnail (16:9 aspect ratio)
                                    "type": "video",  // Type of the content (e.g., video)
                                    "view_count": 0  // Number of views for the video
                                },
                                // Additional video items follow the same structure...
                            ],
                            "visible_items": [  // List of visible items in the gallery
                                0,
                                1,
                                2,
                                3
                            ]
                        }
                    }
                },
                "experiments": {},  // Placeholder for experimental features (empty in this case)
                "fetcher_mode": "voice",  // Indicates the mode of fetching data (e.g., voice)
                "request_id": "ffffffff-ffff-ffff-d5a5-16913359bf22",  // Unique ID for the request
                "session_id": "ffffffff-ffff-ffff-be8a-4d527bb40f8a__ffffffff-ffff-ffff-d5a5-16913359bf22",  // Unique ID for the session
                "session_sequence": 1,  // Sequence number of the session
                "text": "включи один",  // Text of the user's request (e.g., "play one")
                "vins_intent": "mm\tpersonal_assistant\tscenarios\tquasar\tselect_video_from_gallery"  // Intent of the request as interpreted by the VINS system
                "voice_base64_binary": "T2dnUwACAAAAAAAAAABNdW1bAAAAALlo+SwBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAE11bVsBAAAAa81W8wP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAEALAAAAAAAA\nTXVtWwIAAAAh/KZ4Az9NTUiCAf/A/bFRsNdhkg1dtdle7wm6oMIKnAMG6WZ4mkHbSNKTKT6Zb1Cl\n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\nzNSCe69Q76wec8EVoivd+A==\n"
                // Specifies the base64-encoded binary representation of the voice input.
            }
        },
        "request": {  // Start of the second request object
            "expected": {  // Expected response or behavior from the server
                "directives": "client_action:video_play",  // Specifies the action for the client (e.g., play video)
                "intent": "mm.personal_assistant.scenarios.quasar.select_video_from_gallery",  // Indicates the intent of the request (select video from gallery)
                "xfail": true  // Indicates if the request is expected to fail (e.g., for testing purposes)
            },
            "request": {  // Nested request object containing detailed information
                "app_preset": "quasar",  // Specifies the application preset being used
                "device_state": {  // Describes the current state of the device
                    "alarm_state": {  // Information about the device's alarm state
                        "currently_playing": false,  // Indicates whether an alarm is currently playing
                        "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190507T143000Z\r\nDTEND:20190507T143000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190507T143000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T043000Z\r\nDTEND:20190512T043000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T043000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T040000Z\r\nDTEND:20190512T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190518T030000Z\r\nDTEND:20190518T030000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190518T030000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190519T040000Z\r\nDTEND:20190519T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190519T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190525T040000Z\r\nDTEND:20190525T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190525T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190526T040000Z\r\nDTEND:20190526T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190526T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190630T083000Z\r\nDTEND:20190630T083000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190630T083000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190829T160000Z\r\nDTEND:20190829T160000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190829T160000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190913T141000Z\r\nDTEND:20190913T141000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190913T141000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20191013T140000Z\r\nDTEND:20191013T140000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191013T140000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"  // iCalendar data for scheduled alarms
                    },
                    "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190507T143000Z\r\nDTEND:20190507T143000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190507T143000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T043000Z\r\nDTEND:20190512T043000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T043000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190512T040000Z\r\nDTEND:20190512T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190512T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190518T030000Z\r\nDTEND:20190518T030000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190518T030000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190519T040000Z\r\nDTEND:20190519T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190519T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190525T040000Z\r\nDTEND:20190525T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190525T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190526T040000Z\r\nDTEND:20190526T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190526T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190630T083000Z\r\nDTEND:20190630T083000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190630T083000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190829T160000Z\r\nDTEND:20190829T160000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190829T160000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190913T141000Z\r\nDTEND:20190913T141000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190913T141000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20191013T140000Z\r\nDTEND:20191013T140000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191013T140000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",  // Another iCalendar string for alarms state
                    "device_config": {  // Configuration settings for the device
                        "content_settings": "medium",  // Specifies content settings (e.g., medium quality)
                        "spotter": "alisa"  // Indicates the voice assistant being used (e.g., Alisa)
                    },
                    "is_tv_plugged_in": true,  // Indicates whether a TV is connected to the device
                    "last_watched": {  // Information about the last watched media
                        "movies": [],  // List of last watched movies (empty in this case)
                        "tv_shows": [],  // List of last watched TV shows (empty in this case)
                        "videos": [  // List of last watched videos
                            {
                                "play_uri": "https://yastatic.net/video-player/0x0fd98704a3/pages-common/ok/ok.html#html=%3Ciframe%20src%3D%22//ok.ru/videoembed/9542763926%3Fautoplay%3D1%26amp;ya%3D1%22%20frameborder%3D%220%22%20scrolling%3D%22no%22%20allowfullscreen%3D%221%22%20allow%3D%22autoplay;%20fullscreen;%20accelerometer;%20gyroscope;%20picture-in-picture%22%20aria-label%3D%22Video%22%3E%3C/iframe%3E&autoplay=yes&tv=1&clean=true",  // URI for playing the video
                                "progress": {  // Information about the playback progress
                                    "duration": 1227,  // Total duration of the video in seconds
                                    "played": 492  // Duration of the video that has been played in seconds
                                },
                                "provider_item_id": "http://ok.ru/video/9542763926",  // Unique ID of the video from the provider
                                "provider_name": "yavideo",  // Name of the video provider (e.g., Yandex Video)
                                "timestamp": 1572614838  // Timestamp of when the video was last watched
                            },
                            {
                                "play_uri": "youtube://blUGu9fZ3hA",  // URI for playing the video (YouTube)
                                "progress": {  // Information about the playback progress
                                    "duration": 5569,  // Total duration of the video in seconds
                                    "played": 2145  // Duration of the video that has been played in seconds
                                },
                                "provider_item_id": "blUGu9fZ3hA",  // Unique ID of the video from the provider (YouTube video ID)
                                "provider_name": "youtube",  // Name of the video provider (e.g., YouTube)
                                "timestamp": 1572623140  // Timestamp of when the video was last watched
                            }
                        ]
                    },
                    "music": {  // Information about the current music state
                        "currently_playing": {  // Details about the currently playing track
                            "track_id": "45466301",  // Unique ID of the track
                            "track_info": {  // Metadata about the track
                                "albums": [  // List of albums associated with the track
                                    {
                                        "artists": [  // List of artists associated with the album
                                            {
                                                "composer": false,  // Indicates if the artist is a composer
                                                "cover": {  // Cover image details for the artist
                                                    "prefix": "0519833a.a.6103411-1",  // Prefix for the cover image URL
                                                    "type": "from-album-cover",  // Type of cover image
                                                    "uri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%"  // URI for the cover image
                                                },
                                                "genres": [],  // List of genres associated with the artist (empty in this case)
                                                "id": 5908164,  // Unique ID of the artist
                                                "name": "Черный Рояль Самурая",  // Name of the artist
                                                "various": false  // Indicates if the artist is a compilation
                                            }
                                        ],
                                        "available": true,  // Indicates if the album is available
                                        "availableForMobile": true,  // Indicates if the album is available on mobile
                                        "availableForPremiumUsers": true,  // Indicates if the album is available for premium users
                                        "availablePartially": false,  // Indicates if the album is partially available
                                        "bests": [  // List of best tracks in the album
                                            45466306,
                                            45466301,
                                            45466302
                                        ],
                                        "buy": [],  // List of purchase options (empty in this case)
                                        "coverUri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // URI for the album cover
                                        "genre": "newage",  // Genre of the album
                                        "id": 6103411,  // Unique ID of the album
                                        "labels": [  // List of labels associated with the album
                                            {
                                                "id": 1250450,  // Unique ID of the label
                                                "name": "Black Piano Classic"  // Name of the label
                                            }
                                        ],
                                        "ogImage": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // Open Graph image for the album
                                        "recent": false,  // Indicates if the album is recent
                                        "title": "Звуки фортепьяно под звуки природы и леса",  // Title of the album
                                        "trackCount": 11,  // Number of tracks in the album
                                        "trackPosition": {  // Position of the current track in the album
                                            "index": 1,  // Index of the track
                                            "volume": 1  // Volume number of the track
                                        },
                                        "version": "Original Mix",  // Version of the album (e.g., Original Mix)
                                        "veryImportant": false,  // Indicates if the album is very important
                                        "year": 2019  // Year of the album's release
                                    }
                                ],
                                "artists": [  // List of artists associated with the track
                                    {
                                        "composer": false,  // Indicates if the artist is a composer
                                        "cover": {  // Cover image details for the artist
                                            "prefix": "0519833a.a.6103411-1",  // Prefix for the cover image URL
                                            "type": "from-album-cover",  // Type of cover image
                                            "uri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%"  // URI for the cover image
                                        },
                                        "genres": [],  // List of genres associated with the artist (empty in this case)
                                        "id": 5908164,  // Unique ID of the artist
                                        "name": "Черный Рояль Самурая",  // Name of the artist
                                        "various": false  // Indicates if the artist is a compilation
                                    }
                                ],
                                "available": true,  // Indicates if the track is available
                                "availableForPremiumUsers": true,  // Indicates if the track is available for premium users
                                "availableFullWithoutPermission": false,  // Indicates if the track is fully available without permission
                                "batchId": "sync-93f5db4f-b710-4796-9098-f17f60c920c2",  // Batch ID for synchronization
                                "batchInfo": {  // Information about the batch
                                    "index": 0,  // Index of the batch
                                    "rid": "1572614598593874-1501879132-megamind-sas-34-vins",  // Unique ID for the batch
                                    "type": "onDemand"  // Type of the batch (e.g., on-demand)
                                },
                                "coverUri": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // URI for the track cover
                                "durationMs": 107000,  // Duration of the track in milliseconds
                                "fileSize": 2569195,  // File size of the track in bytes
                                "id": "45466301",  // Unique ID of the track
                                "lyricsAvailable": false,  // Indicates if lyrics are available for the track
                                "major": {  // Major information about the track
                                    "id": 134,  // Unique ID of the major
                                    "name": "ELECTRONIC_MUSIC_DISTRIBUTION"  // Name of the major
                                },
                                "normalization": {  // Normalization settings for the track
                                    "gain": -8.07,  // Gain value for normalization
                                    "peak": 32393  // Peak value for normalization
                                },
                                "ogImage": "avatars.yandex.net/get-music-content/97284/0519833a.a.6103411-1/%%",  // Open Graph image for the track
                                "previewDurationMs": 30000,  // Duration of the track preview in milliseconds
                                "realId": "45466301",  // Real ID of the track
                                "rememberPosition": false,  // Indicates if the track position should be remembered
                                "storageDir": "1445069_81617160.67748721.1.45466301",  // Storage directory for the track
                                "title": "Фортепьяно и звуки леса №1",  // Title of the track
                                "type": "music",  // Type of the track (e.g., music)
                                "version": "Original Mix"  // Version of the track (e.g., Original Mix)
                            }
                        },
                        "player": {  // Information about the music player
                            "pause": true,  // Indicates if the player is paused
                            "timestamp": 1572614604  // Timestamp of when the player state was last updated
                        },
                        "playlist_owner": "",  // Owner of the playlist (empty in this case)
                        "session_id": "tRJSHcPj"  // Unique session ID for the music player
                    },
                    "sound_level": 5,  // Current sound level of the device
                    "sound_muted": false,  // Indicates if the sound is muted
                    "timers": {  // Information about active timers
                        "active_timers": []  // List of active timers (empty in this case)
                    },
                    "video": {  // Information about the current video state
                        "current_screen": "gallery",  // Indicates the current screen being displayed (e.g., gallery)
                        "screen_state": {  // State of the current screen
                            "debug_info": {  // Debug information for the screen
                                "url": "/video/search?assistant=1&family=moderate&g=1.dg.20.1.-1&gta=qproxy&json_dump=searchdata&noredirect=1&rearr=forced_player_device%3Dquasar&rearr=scheme_Local/VideoSnippets/ReplaceVhDups%3D0&rearr=forced_qproxy_player%3D1&text=3+%D0%BA%D0%BE%D1%82%D0%B0",  // URL for the video search
                                "ya_video_request": "3 кота"  // Text of the video search request (e.g., "3 кота")
                            },
                            "items": [  // List of items in the gallery
                                {
                                    "available": 1,  // Indicates if the video is available
                                    "duration": 3865,  // Duration of the video in seconds
                                    "name": "Три кота - Сборник зимних серий",  // Name of the video
                                    "normalized_name": "3 кота - сборник зимних серий",  // Normalized name of the video
                                    "play_uri": "youtube://-E0JW1ONGPQ",  // URI for playing the video (YouTube)
                                    "price_from": 0,  // Price of the video (free in this case)
                                    "provider_info": [  // Information about the video provider
                                        {
                                            "available": 1,  // Indicates if the video is available
                                            "provider_item_id": "-E0JW1ONGPQ",  // Unique ID of the video from the provider
                                            "provider_name": "youtube",  // Name of the video provider (e.g., YouTube)
                                            "type": "video"  // Type of the content (e.g., video)
                                        }
                                    ],
                                    "provider_item_id": "-E0JW1ONGPQ",  // Unique ID of the video from the provider
                                    "provider_name": "youtube",  // Name of the video provider (e.g., YouTube)
                                    "source_host": "www.youtube.com",  // Host of the video source (e.g., YouTube)
                                    "thumbnail_url_16x9": "https://avatars.mds.yandex.net/get-vthumb/228771/e45fc9725cf00fa1b6fd00cb32224e60/800x360",  // URL for the video thumbnail (16:9 aspect ratio)
                                    "type": "video",  // Type of the content (e.g., video)
                                    "view_count": 0  // Number of views for the video
                                },
                                // Additional video items follow the same structure...
                            ],
                            "visible_items": [  // List of visible items in the gallery
                                0,
                                1,
                                2,
                                3
                            ]
                        }
                    }
                },
                "experiments": {},  // Placeholder for experimental features (empty in this case)
                "fetcher_mode": "voice",  // Indicates the mode of fetching data (e.g., voice)
                "request_id": "ffffffff-ffff-ffff-d5a5-16913359bf22",  // Unique ID for the request
                "session_id": "ffffffff-ffff-ffff-be8a-4d527bb40f8a__ffffffff-ffff-ffff-d5a5-16913359bf22",  // Unique ID for the session
                "session_sequence": 1,  // Sequence number of the session
                "text": "включи один",  // Text of the user's request (e.g., "play one")
                "vins_intent": "mm\tpersonal_assistant\tscenarios\tquasar\tselect_video_from_gallery"  // Intent of the request as interpreted by the VINS system
                "voice_base64_binary": "T2dnUwACAAAAAAAAAABuMJ4rAAAAAB/rXQQBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAG4wnisBAAAAie2ZJQP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAEALAAAAAAAA\nbjCeKwIAAABfWX3vAz0/NkgB1bLJgMr5K5mqAe3HqmU3VRBgYSz7Any7iesL2yImflBUrp9Y7xJr\n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\nwluG6kbszqSPLjo=\n"
                // Specifies the base64-encoded binary representation of the voice input.
            }
        }
    }
]
```
