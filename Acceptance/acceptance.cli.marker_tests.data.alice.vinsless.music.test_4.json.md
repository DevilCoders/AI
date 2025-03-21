```json
[
    {
        "context": {
    // The `context` block contains information about the context of the request, including the expected response and the request details.

    "expected": {
        // The `expected` block defines the expected behavior or response for the request.

        "directives": "client_action:audio_play, server_action:@@mm_stack_engine_get_next",
        // Specifies the expected directives in the response.  
        // The client is expected to perform an audio play action, and the server is expected to execute the `mm_stack_engine_get_next` action.

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

                "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190117T050000Z\r\nDTEND:20190117T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190117T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190118T040000Z\r\nDTEND:20190118T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190118T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190129T040000Z\r\nDTEND:20190129T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190129T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190130T040000Z\r\nDTEND:20190130T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190130T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190131T060000Z\r\nDTEND:20190131T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190131T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190201T060000Z\r\nDTEND:20190201T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190201T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190204T050000Z\r\nDTEND:20190204T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190204T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"
                // Specifies the iCalendar data for the alarm, including the start times and triggers for multiple alarms.
            },
            "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190117T050000Z\r\nDTEND:20190117T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190117T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190118T040000Z\r\nDTEND:20190118T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190118T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190129T040000Z\r\nDTEND:20190129T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190129T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190130T040000Z\r\nDTEND:20190130T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190130T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190131T060000Z\r\nDTEND:20190131T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190131T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190201T060000Z\r\nDTEND:20190201T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190201T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190204T050000Z\r\nDTEND:20190204T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190204T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",
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

                    "track_id": "2192047",
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

                                            "prefix": "5d230583.a.216929-1",
                                            // Specifies the prefix for the cover art URL.

                                            "type": "from-album-cover",
                                            // Specifies the type of cover art.

                                            "uri": "avatars.yandex.net/get-music-content/41288/5d230583.a.216929-1/%%"
                                            // Specifies the URI for the cover art.
                                        },
                                        "genres": [],
                                        // An empty array indicating no genres are associated with the artist.

                                        "id": 282398,
                                        // Specifies the ID of the artist.

                                        "name": "Gregorian",
                                        // Specifies the name of the artist.

                                        "various": false
                                        // Indicates whether the artist is a "various artists" placeholder (false in this case).
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

                                "bests": [
                                    2192048,
                                    2192036,
                                    2192045
                                ],
                                // Specifies the IDs of the best tracks in the album.

                                "buy": [],
                                // An empty array indicating no purchase options are available.

                                "coverUri": "avatars.yandex.net/get-music-content/41288/5d230583.a.216929-1/%%",
                                // Specifies the URI for the album cover.

                                "genre": "newage",
                                // Specifies the genre of the album.

                                "id": 216929,
                                // Specifies the ID of the album.

                                "labels": [
                                    {
                                        // The `labels` array contains information about the labels associated with the album.

                                        "id": 35880,
                                        // Specifies the ID of the label.

                                        "name": "Союз Мьюзик"
                                        // Specifies the name of the label.
                                    }
                                ],
                                // End of the `labels` array.

                                "ogImage": "avatars.yandex.net/get-music-content/41288/5d230583.a.216929-1/%%",
                                // Specifies the Open Graph image for the album.

                                "recent": false,
                                // Indicates whether the album is recent.

                                "title": "Best Of 1990 - 2010",
                                // Specifies the title of the album.

                                "trackCount": 18,
                                // Specifies the number of tracks in the album.

                                "trackPosition": {
                                    // The `trackPosition` block describes the position of the track in the album.

                                    "index": 1,
                                    // Specifies the index of the track.

                                    "volume": 1
                                    // Specifies the volume of the track.
                                },
                                "veryImportant": false,
                                // Indicates whether the album is marked as very important.

                                "year": 2011
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

                                    "prefix": "5d230583.a.216929-1",
                                    // Specifies the prefix for the cover art URL.

                                    "type": "from-album-cover",
                                    // Specifies the type of cover art.

                                    "uri": "avatars.yandex.net/get-music-content/41288/5d230583.a.216929-1/%%"
                                    // Specifies the URI for the cover art.
                                },
                                "genres": [],
                                // An empty array indicating no genres are associated with the artist.

                                "id": 282398,
                                // Specifies the ID of the artist.

                                "name": "Gregorian",
                                // Specifies the name of the artist.

                                "various": false
                                // Indicates whether the artist is a "various artists" placeholder (false in this case).
                            }
                        ],
                        // End of the `artists` array.

                        "available": true,
                        // Indicates whether the track is available.

                        "availableForPremiumUsers": true,
                        // Indicates whether the track is available for premium users.

                        "availableFullWithoutPermission": false,
                        // Indicates whether the track is available in full without permission.

                        "batchId": "sync-2f01ef08-8f2e-4641-976e-05fb5512c6c2",
                        // Specifies the batch ID for the track.

                        "batchInfo": {
                            // The `batchInfo` block contains information about the batch.

                            "general": false,
                            // Indicates whether the batch is general (false in this case).

                            "rid": "db281c3c-afa6-4a41-b6fa-74a8c7a9884d",
                            // Specifies the request ID for the batch.

                            "type": "dynamic"
                            // Specifies the type of the batch (dynamic in this case).
                        },
                        "coverUri": "avatars.yandex.net/get-music-content/41288/5d230583.a.216929-1/%%",
                        // Specifies the URI for the track cover.

                        "durationMs": 214130,
                        // Specifies the duration of the track in milliseconds.

                        "fileSize": 5140270,
                        // Specifies the file size of the track in bytes.

                        "id": "2192047",
                        // Specifies the ID of the track.

                        "lyricsAvailable": true,
                        // Indicates whether lyrics are available for the track.

                        "major": {
                            // The `major` block contains information about the major label.

                            "id": 86,
                            // Specifies the ID of the major label.

                            "name": "SOYUZ_MUSIC"
                            // Specifies the name of the major label.
                        },
                        "normalization": {
                            // The `normalization` block contains information about audio normalization.

                            "gain": -4.48,
                            // Specifies the gain for audio normalization.

                            "peak": 32766
                            // Specifies the peak level for audio normalization.
                        },
                        "ogImage": "avatars.yandex.net/get-music-content/41288/5d230583.a.216929-1/%%",
                        // Specifies the Open Graph image for the track.

                        "previewDurationMs": 30000,
                        // Specifies the duration of the track preview in milliseconds.

                        "realId": "2192047",
                        // Specifies the real ID of the track.

                        "rememberPosition": false,
                        // Indicates whether the playback position should be remembered.

                        "storageDir": "63121_94650487.2860439.2192047",
                        // Specifies the storage directory for the track.

                        "title": "So Sad",
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

                    "timestamp": 1573254869
                    // Specifies the timestamp of the player's state.
                },
                "playlist_owner": "",
                // Specifies the owner of the playlist (empty in this case).

                "session_id": "RinUB68j"
                // Specifies the session ID for the music playback.
            },
            "sound_level": 2,
            // Specifies the sound level of the device, set to 2.

            "sound_muted": false,
            // Indicates whether the sound is muted (false in this case).

            "timers": {
                // The `timers` block describes the state of timers on the device.

                "active_timers": []
                // An empty array indicating no active timers.
            },
            "video": {
                // The `video` block describes the state of video playback.

                "current_screen": "music_player"
                // Specifies the current screen for video playback as `music_player`.
            }
        },
        // End of the `device_state` block.

        "experiments": {},
        // The `experiments` block describes any active experiments.  
        // This is currently empty.

        "fetcher_mode": "voice",
        // Specifies the fetcher mode as `voice`, indicating that the request is voice-based.

        "request_id": "ffffffff-ffff-ffff-acc5-029377e820ab",
        // Specifies the unique ID of the request.

        "session_id": "ffffffff-ffff-ffff-acc5-029377e820ab__ffffffff-ffff-ffff-74a8-cc3aa3383f2f",
        // Specifies the unique ID of the session.

        "session_sequence": 0,
        // Specifies the sequence number of the session.

        "text": "включи нам веселую музыку",
        // Specifies the text of the request, which translates to "turn on some fun music for us."

        "vins_intent": "personal_assistant\tscenarios\tvinsless\tmusic",
        // Specifies the Vins intent, which is related to music scenarios.

        "voice_base64_binary": "T2dnUwACAAAAAAAAAABMDVs7AAAAAPnx2jwBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAEwNWzsBAAAAc8LS2AP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAMADAAAAAAAA\nTA1bOwIAAADg4ULuATFIAjFPBgvtjvqehHs94ygLqdfKfWKaKUB7k0/ma+aFWFEqN1tLn0RPHGao\n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\n"
        // Specifies the base64-encoded binary representation of the voice input.
    }
},
    {
    "request": {  // Start of the request object
        "expected": {  // Expected response or behavior from the server
            "directives": "client_action:audio_play, server_action:@@mm_stack_engine_get_next",  // Specifies actions for the client and server
            "intent": "personal_assistant.scenarios.music_play"  // Indicates the intent of the request (music playback)
        },
        "request": {  // Nested request object containing detailed information
            "app_preset": "quasar",  // Specifies the application preset being used
            "device_state": {  // Describes the current state of the device
                "alarm_state": {  // Information about the device's alarm state
                    "currently_playing": false,  // Indicates whether an alarm is currently playing
                    "icalendar": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190117T050000Z\r\nDTEND:20190117T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190117T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190118T040000Z\r\nDTEND:20190118T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190118T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190129T040000Z\r\nDTEND:20190129T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190129T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190130T040000Z\r\nDTEND:20190130T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190130T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190131T060000Z\r\nDTEND:20190131T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190131T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190201T060000Z\r\nDTEND:20190201T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190201T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190204T050000Z\r\nDTEND:20190204T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190204T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n"  // iCalendar data for scheduled alarms
                },
                "alarms_state": "BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//Yandex LTD//NONSGML Quasar//EN\r\nBEGIN:VEVENT\r\nDTSTART:20190117T050000Z\r\nDTEND:20190117T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190117T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190118T040000Z\r\nDTEND:20190118T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190118T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190129T040000Z\r\nDTEND:20190129T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190129T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190130T040000Z\r\nDTEND:20190130T040000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190130T040000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190131T060000Z\r\nDTEND:20190131T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190131T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190201T060000Z\r\nDTEND:20190201T060000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190201T060000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nBEGIN:VEVENT\r\nDTSTART:20190204T050000Z\r\nDTEND:20190204T050000Z\r\nBEGIN:VALARM\r\nTRIGGER;VALUE=DATE-TIME:20190204T050000Z\r\nACTION:AUDIO\r\nEND:VALARM\r\nEND:VEVENT\r\nEND:VCALENDAR\r\n",  // Another iCalendar string for alarms state
                "device_config": {  // Configuration settings for the device
                    "content_settings": "without",  // Specifies content settings
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
                        "track_id": "28098621",  // Unique ID of the track
                        "track_info": {  // Metadata about the track
                            "albums": [  // List of albums associated with the track
                                {
                                    "artists": [  // List of artists associated with the album
                                        {
                                            "composer": false,  // Indicates if the artist is a composer
                                            "cover": {  // Cover image details for the artist
                                                "prefix": "d88160a4.a.7671063-1",  // Prefix for the cover image URL
                                                "type": "from-album-cover",  // Type of cover image
                                                "uri": "avatars.yandex.net/get-music-content/139444/d88160a4.a.7671063-1/%%"  // URI for the cover image
                                            },
                                            "genres": [],  // List of genres associated with the artist (empty in this case)
                                            "id": 171,  // Unique ID of the artist
                                            "name": "сборник",  // Name of the artist
                                            "various": true  // Indicates if the artist is a compilation
                                        }
                                    ],
                                    "available": true,  // Indicates if the album is available
                                    "availableForMobile": true,  // Indicates if the album is available on mobile
                                    "availableForPremiumUsers": true,  // Indicates if the album is available for premium users
                                    "availablePartially": false,  // Indicates if the album is partially available
                                    "bests": [  // List of best tracks in the album
                                        23616681,
                                        28098632,
                                        28098619
                                    ],
                                    "buy": [],  // List of purchase options (empty in this case)
                                    "coverUri": "avatars.yandex.net/get-music-content/42108/cceb225f.a.3356237-1/%%",  // URI for the album cover
                                    "genre": "ruspop",  // Genre of the album
                                    "id": 3356237,  // Unique ID of the album
                                    "labels": [  // List of labels associated with the album
                                        {
                                            "id": 2685,  // Unique ID of the label
                                            "name": "United Music Group"  // Name of the label
                                        }
                                    ],
                                    "ogImage": "avatars.yandex.net/get-music-content/42108/cceb225f.a.3356237-1/%%",  // Open Graph image for the album
                                    "recent": false,  // Indicates if the album is recent
                                    "releaseDate": "2015-08-16T00:00:00+03:00",  // Release date of the album
                                    "title": "50 лучших хитов",  // Title of the album
                                    "trackCount": 49,  // Number of tracks in the album
                                    "trackPosition": {  // Position of the current track in the album
                                        "index": 12,  // Index of the track
                                        "volume": 1  // Volume number of the track
                                    },
                                    "type": "compilation",  // Type of the album (e.g., compilation)
                                    "veryImportant": false,  // Indicates if the album is very important
                                    "year": 2015  // Year of the album's release
                                }
                            ],
                            "artists": [  // List of artists associated with the track
                                {
                                    "composer": false,  // Indicates if the artist is a composer
                                    "cover": {  // Cover image details for the artist
                                        "prefix": "a6d84950.p.587138/",  // Prefix for the cover image URL
                                        "type": "from-artist-photos",  // Type of cover image
                                        "uri": "avatars.yandex.net/get-music-content/28589/a6d84950.p.587138/%%"  // URI for the cover image
                                    },
                                    "genres": [],  // List of genres associated with the artist (empty in this case)
                                    "id": 587138,  // Unique ID of the artist
                                    "name": "Доминик Джокер",  // Name of the artist
                                    "various": false  // Indicates if the artist is a compilation
                                }
                            ],
                            "available": true,  // Indicates if the track is available
                            "availableForPremiumUsers": true,  // Indicates if the track is available for premium users
                            "availableFullWithoutPermission": false,  // Indicates if the track is fully available without permission
                            "batchId": "sync-6dfe6c73-83f7-426f-93a4-c4fbcc333b3b",  // Batch ID for synchronization
                            "batchInfo": {  // Information about the batch
                                "general": false,  // Indicates if the batch is general
                                "rid": "907c0df6-fd4b-49bc-8b3e-3873f56aa330",  // Unique ID for the batch
                                "type": "dynamic"  // Type of the batch
                            },
                            "coverUri": "avatars.yandex.net/get-music-content/42108/cceb225f.a.3356237-1/%%",  // URI for the track cover
                            "durationMs": 223220,  // Duration of the track in milliseconds
                            "fileSize": 5358445,  // File size of the track in bytes
                            "id": "28098621",  // Unique ID of the track
                            "lyricsAvailable": true,  // Indicates if lyrics are available for the track
                            "major": {  // Major information about the track
                                "id": 123,  // Unique ID of the major
                                "name": "IRICOM"  // Name of the major
                            },
                            "normalization": {  // Normalization settings for the track
                                "gain": -7.69,  // Gain value for normalization
                                "peak": 32766  // Peak value for normalization
                            },
                            "ogImage": "avatars.yandex.net/get-music-content/42108/cceb225f.a.3356237-1/%%",  // Open Graph image for the track
                            "previewDurationMs": 30000,  // Duration of the track preview in milliseconds
                            "realId": "28098621",  // Real ID of the track
                            "rememberPosition": false,  // Indicates if the track position should be remembered
                            "storageDir": "59965_927da985.41926687.1.28098621",  // Storage directory for the track
                            "title": "Если ты со мной",  // Title of the track
                            "type": "music"  // Type of the track (e.g., music)
                        }
                    },
                    "player": {  // Information about the music player
                        "pause": false  // Indicates if the player is paused
                    },
                    "playlist_owner": "",  // Owner of the playlist (empty in this case)
                    "session_id": "Dbp68fxO"  // Unique session ID for the music player
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
            "request_id": "ffffffff-ffff-ffff-74a8-cc3aa3383f2f",  // Unique ID for the request
            "session_id": "ffffffff-ffff-ffff-acc5-029377e820ab__ffffffff-ffff-ffff-74a8-cc3aa3383f2f",  // Unique ID for the session
            "session_sequence": 1,  // Sequence number of the session
            "text": "включи веселую музыку",  // Text of the user's request (e.g., "play happy music")
            "vins_intent": "personal_assistant\tscenarios\tvinsless\tmusic"  // Intent of the request as interpreted by the VINS system
            "voice_base64_binary": "T2dnUwACAAAAAAAAAAAPq/1QAAAAAJ5zADYBE09wdXNIZWFkAQEAAIA+AAAAAABPZ2dTAAAAAAAA\nAAAAAA+r/VABAAAAlPQejgP///5PcHVzVGFncwkAAABTcGVlY2hLaXQBAAAAIwAAAEVOQ09ERVI9\nU3BlZWNoS2l0IE1vYmlsZSBTREsgdjMuMzAuNQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\nAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE9nZ1MAAMADAAAAAAAA\nD6v9UAIAAAAVgK/NATBIASCD7jHlOilLaq0vxXn4zJSQO+bTCeXCBqoXH9zA/gqybaY8EZylpGJn\n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\n"
            // Specifies the base64-encoded binary representation of the voice input.
        }
    }
}
    }
]
```
