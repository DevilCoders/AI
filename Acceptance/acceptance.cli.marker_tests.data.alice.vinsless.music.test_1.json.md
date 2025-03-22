```json
[
    // The JSON array contains one or more objects, each representing a test case or request.

    {
        // The first object in the array represents a specific test case or request.

        "request": {
            // The `request` block contains details about the request and its expected response.

            "expected": {
                // The `expected` block defines the expected behavior or response for the request.

                "directives": "client_action:audio_play, server_action:@@mm_stack_engine_get_next",
                // Specifies the expected directives in the response.  
                // In this case, the client is expected to perform an audio play action, and the server is expected to execute the `mm_stack_engine_get_next` action.

                "intent": "personal_assistant.scenarios.music_play"
                // Specifies the expected intent of the request, which is `personal_assistant.scenarios.music_play`.  
                // This indicates that the request is related to playing music.
            },
            "request": {
                // The `request` block contains details about the request itself.

                "app_preset": "quasar",
                // Specifies the app preset as `quasar`, which likely defines the configuration or behavior of the application.

                "device_state": {
                    // The `device_state` block describes the state of the device making the request.

                    "alarm_state": {
                        // The `alarm_state` block describes the state of the device's alarm.

                        "currently_playing": false,
                        // Indicates that no alarm is currently playing.

                        "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191028T040000Z\r\nDTEND:20191028T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191028T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"
                        // Specifies the iCalendar data for the alarm, including the start time and trigger.
                    },
                    "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20191028T040000Z\r\nDTEND:20191028T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20191028T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",
                    // Specifies the overall state of alarms on the device, using iCalendar format.

                    "device_config": {
                        // The `device_config` block describes the configuration of the device.

                        "content_settings": "without",
                        // Specifies the content settings for the device, which is set to `without`.

                        "spotter": "alisa"
                        // Specifies the spotter (wake word detection) as `alisa`.
                    },
                    "is_tv_plugged_in": false,
                    // Indicates whether a TV is plugged into the device (false in this case).

                    "last_watched": {
                        // The `last_watched` block describes the last watched movies, TV shows, and videos.

                        "movies": [],
                        // An empty array indicating no recently watched movies.

                        "tv_shows": [],
                        // An empty array indicating no recently watched TV shows.

                        "videos": []
                        // An empty array indicating no recently watched videos.
                    },
                    "music": {
                        // The `music` block describes the current state of music playback.

                        "currently_playing": {
                            // The `currently_playing` block describes the currently playing track.

                            "track_id": "36722733",
                            // Specifies the ID of the currently playing track.

                            "track_info": {
                                // The `track_info` block contains detailed information about the track.

                                "albums": [
                                    {
                                        // The `albums` array contains information about the album(s) the track belongs to.

                                        "artists": [
                                            {
                                                // The `artists` array contains information about the artists associated with the album.

                                                "composer": false,
                                                // Indicates whether the artist is a composer (false in this case).

                                                "cover": {
                                                    // The `cover` block describes the cover art for the artist.

                                                    "prefix": "6ae45b69.a.4631286-1",
                                                    // Specifies the prefix for the cover art URL.

                                                    "type": "from-album-cover",
                                                    // Specifies the type of cover art.

                                                    "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                                    // Specifies the URI for the cover art.
                                                },
                                                "genres": [],
                                                // An empty array indicating no genres are associated with the artist.

                                                "id": 4118336,
                                                // Specifies the ID of the artist.

                                                "name": "Bolier",
                                                // Specifies the name of the artist.

                                                "various": false
                                                // Indicates whether the artist is a "various artists" placeholder (false in this case).
                                            },
                                            {
                                                // Additional artist information.
                                                "composer": false,
                                                "cover": {
                                                    "prefix": "6ae45b69.a.4631286-1",
                                                    "type": "from-album-cover",
                                                    "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                                },
                                                "genres": [],
                                                "id": 3084440,
                                                "name": "Arem Ozguc",
                                                "various": false
                                            },
                                            {
                                                // Additional artist information.
                                                "composer": false,
                                                "cover": {
                                                    "prefix": "6ae45b69.a.4631286-1",
                                                    "type": "from-album-cover",
                                                    "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                                },
                                                "genres": [],
                                                "id": 781708,
                                                "name": "Arman Aydin",
                                                "various": false
                                            },
                                            {
                                                // Additional artist information.
                                                "composer": false,
                                                "cover": {
                                                    "prefix": "6ae45b69.a.4631286-1",
                                                    "type": "from-album-cover",
                                                    "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                                },
                                                "genres": [],
                                                "id": 5292707,
                                                "name": "NBLM",
                                                "various": false
                                            }
                                        ],
                                        // End of the `artists` array.

                                        "available": true,
                                        // Indicates whether the album is available.

                                        "availableForMobile": true,
                                        // Indicates whether the album is available for mobile devices.

                                        "availableForPremiumUsers": true,
                                        // Indicates whether the album is available for premium users.

                                        "availablePartially": false,
                                        // Indicates whether the album is partially available.

                                        "bests": [],
                                        // An empty array indicating no best tracks are associated with the album.

                                        "buy": [],
                                        // An empty array indicating no purchase options are available.

                                        "coverUri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%",
                                        // Specifies the URI for the album cover.

                                        "genre": "dance",
                                        // Specifies the genre of the album.

                                        "id": 4631286,
                                        // Specifies the ID of the album.

                                        "labels": [
                                            {
                                                // The `labels` array contains information about the labels associated with the album.

                                                "id": 1218126,
                                                // Specifies the ID of the label.

                                                "name": "EMI - Kent Elektronik Sanayi ve Ticaret"
                                                // Specifies the name of the label.
                                            }
                                        ],
                                        // End of the `labels` array.

                                        "ogImage": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%",
                                        // Specifies the Open Graph image for the album.

                                        "recent": false,
                                        // Indicates whether the album is recent.

                                        "releaseDate": "2017-08-25T00:00:00+03:00",
                                        // Specifies the release date of the album.

                                        "title": "Imagine",
                                        // Specifies the title of the album.

                                        "trackCount": 1,
                                        // Specifies the number of tracks in the album.

                                        "trackPosition": {
                                            // The `trackPosition` block describes the position of the track in the album.

                                            "index": 1,
                                            // Specifies the index of the track.

                                            "volume": 1
                                            // Specifies the volume of the track.
                                        },
                                        "type": "single",
                                        // Specifies the type of the album (single in this case).

                                        "veryImportant": false,
                                        // Indicates whether the album is marked as very important.

                                        "year": 2017
                                        // Specifies the year of the album's release.
                                    }
                                ],
                                // End of the `albums` array.

                                "artists": [
                                    {
                                        // The `artists` array contains information about the artists associated with the track.

                                        "composer": false,
                                        // Indicates whether the artist is a composer (false in this case).

                                        "cover": {
                                            // The `cover` block describes the cover art for the artist.

                                            "prefix": "6ae45b69.a.4631286-1",
                                            // Specifies the prefix for the cover art URL.

                                            "type": "from-album-cover",
                                            // Specifies the type of cover art.

                                            "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                            // Specifies the URI for the cover art.
                                        },
                                        "genres": [],
                                        // An empty array indicating no genres are associated with the artist.

                                        "id": 4118336,
                                        // Specifies the ID of the artist.

                                        "name": "Bolier",
                                        // Specifies the name of the artist.

                                        "various": false
                                        // Indicates whether the artist is a "various artists" placeholder (false in this case).
                                    },
                                    {
                                        // Additional artist information.
                                        "composer": false,
                                        "cover": {
                                            "prefix": "6ae45b69.a.4631286-1",
                                            "type": "from-album-cover",
                                            "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                        },
                                        "genres": [],
                                        "id": 3084440,
                                        "name": "Arem Ozguc",
                                        "various": false
                                    },
                                    {
                                        // Additional artist information.
                                        "composer": false,
                                        "cover": {
                                            "prefix": "6ae45b69.a.4631286-1",
                                            "type": "from-album-cover",
                                            "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                        },
                                        "genres": [],
                                        "id": 781708,
                                        "name": "Arman Aydin",
                                        "various": false
                                    },
                                    {
                                        // Additional artist information.
                                        "composer": false,
                                        "cover": {
                                            "prefix": "6ae45b69.a.4631286-1",
                                            "type": "from-album-cover",
                                            "uri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%"
                                        },
                                        "genres": [],
                                        "id": 5292707,
                                        "name": "NBLM",
                                        "various": false
                                    }
                                ],
                                // End of the `artists` array.

                                "available": true,
                                // Indicates whether the track is available.

                                "availableForPremiumUsers": true,
                                // Indicates whether the track is available for premium users.

                                "availableFullWithoutPermission": false,
                                // Indicates whether the track is available in full without permission.

                                "batchId": "sync-699d4301-49bd-4031-96c4-7223f8104a90",
                                // Specifies the batch ID for the track.

                                "batchInfo": {
                                    // The `batchInfo` block contains information about the batch.

                                    "index": 2,
                                    // Specifies the index of the track in the batch.

                                    "rid": "b80c5754-0866-4532-88b0-687250e7a0d5",
                                    // Specifies the request ID for the batch.

                                    "type": "onDemand"
                                    // Specifies the type of the batch (onDemand in this case).
                                },
                                "coverUri": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%",
                                // Specifies the URI for the track cover.

                                "durationMs": 170210,
                                // Specifies the duration of the track in milliseconds.

                                "fileSize": 4085759,
                                // Specifies the file size of the track in bytes.

                                "id": "36722733",
                                // Specifies the ID of the track.

                                "lyricsAvailable": true,
                                // Indicates whether lyrics are available for the track.

                                "major": {
                                    // The `major` block contains information about the major label.

                                    "id": 1,
                                    // Specifies the ID of the major label.

                                    "name": "UNIVERSAL_MUSIC"
                                    // Specifies the name of the major label.
                                },
                                "normalization": {
                                    // The `normalization` block contains information about audio normalization.

                                    "gain": -9.86,
                                    // Specifies the gain for audio normalization.

                                    "peak": 32766
                                    // Specifies the peak level for audio normalization.
                                },
                                "ogImage": "avatars.yandex.net/get-music-content/163479/6ae45b69.a.4631286-1/%%",
                                // Specifies the Open Graph image for the track.

                                "previewDurationMs": 30000,
                                // Specifies the duration of the track preview in milliseconds.

                                "realId": "36722733",
                                // Specifies the real ID of the track.

                                "rememberPosition": false,
                                // Indicates whether the playback position should be remembered.

                                "storageDir": "231634_8bf1949c.55095882.1.36722733",
                                // Specifies the storage directory for the track.

                                "title": "Imagine",
                                // Specifies the title of the track.

                                "type": "music"
                                // Specifies the type of the track (music in this case).
                            }
                        },
                        // End of the `currently_playing` block.

                        "player": {
                            // The `player` block describes the state of the music player.

                            "pause": true,
                            // Indicates whether the player is paused.

                            "timestamp": 1572690018
                            // Specifies the timestamp of the player's state.
                        },
                        "playlist_owner": "671836245",
                        // Specifies the owner of the playlist.

                        "session_id": "VjfITLCP"
                        // Specifies the session ID for the music playback.
                    },
                    "sound_level": 2,
                    // Specifies the sound level of the device.

                    "sound_muted": false,
                    // Indicates whether the sound is muted.

                    "timers": {
                        // The `timers` block describes the state of timers on the device.

                        "active_timers": []
                        // An empty array indicating no active timers.
                    },
                    "video": {
                        // The `video` block describes the state of video playback.

                        "current_screen": "main"
                        // Specifies the current screen for video playback.
                    }
                },
                // End of the `device_state` block.

                "experiments": {},
                // The `experiments` block describes any active experiments.  
                // This is currently empty.

                "fetcher_mode": "voice",
                // Specifies the fetcher mode as `voice`, indicating that the request is voice-based.

                "request_id": "ffffffff-ffff-ffff-afef-347f73f284ae",
                // Specifies the unique ID of the request.

                "session_id": "ffffffff-ffff-ffff-afef-347f73f284ae",
                // Specifies the unique ID of the session.

                "session_sequence": 0,
                // Specifies the sequence number of the session.

                "text": "включи плейлист дня",
                // Specifies the text of the request, which translates to "turn on the playlist of the day."

                "vins_intent": "personal_assistant\tscenarios\tvinsless\tmusic",
                // Specifies the Vins intent, which is related to music scenarios.

                "voice_base64_binary": "T2dnUwACAAAAAAAAAADwZFtHAAAAAIzFqCcBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAPBkW0cBAAAAQ2Bq+AP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAIAHAAAAAAAA\n8GRbRwIAAAAxWuw2AjM2SIBXAlUyNw9uGa7Sa7qHk7RSyuQ2OICn+E6rWbTdjx+MxVcGjpMiBQkK\n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\n"
                // Specifies the base64-encoded binary representation of the voice input.
            }
        }
    }
]
```
