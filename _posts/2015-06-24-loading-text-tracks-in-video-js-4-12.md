---
title: Loading text tracks in video.js 4.12
author: walsh9
layout: post
categories:
  - notes
  - projects
---
I recently updated [videojs-transcript][1], a videojs plugin that automatically generates an interactive transcript from video captions, to work with video.js 4.12.

There was a [big overhaul][2] of how text tracks for captions work in vjs 4.12. The methods on text tracks changed to be more in line with the [HTML 5 Text Track API][3]. The details here will probably only be interesting if you are trying to make a plugin for video.js that uses text tracks, but here are some of the changes I ran into.

**Text tracks are now contained in a `TextTrackList` instead of a plain array.**

I was using `.foreach()` to iterate through the tracks. I had to change to a `for` loop. No problem.

**No more `.load()` method on text tracks.**

I want videojs to load and parse the subtitles for me without me switching the currently active track. Now, to load up non-active tracks, I need to change the `.mode` property on the track I want to `'hidden'`. The track is then loaded but not displayed. Cool.

**No more `'loaded'` event or `.readyState` property to tell when a track is loaded.**

This part is probably the hackiest workaround. I have to use a `setTimeout()` loop to check that a track's `.activeCues` property isn't `null`. The `.activeCues` property [should be null until the track is loaded][4]. Not ideal but it works, and [video.js itself currently uses something similar to load chapter titles][5].

So here's the old way I used to load text tracks:

```javascript
var getTrackAndDoSomething = function(track) {

    // A function to call when the track is ready. 
    var doSomethingWithTheTrack = function() {
        /* do fun stuff with the ready track here */
    });

    // .readyState() == 2 means the track is loaded.
    // If the track isn't loaded...
    if (track.readyState() !==2) { 

        // Load the track
        track.load();

        // Do stuff when we get the 'loaded' callback.
        track.on('loaded', doSomethingWithTheTrack);

    // If the track is loaded, do stuff now.
    } else {
       doSomethingWithTheTrack();
    }
};
```

And here's the new way:

```javascript
var getTrackAndDoSomething = function(track) {

    // .activeCues should be null until the track is loaded.
    // If the track isn't loaded...
    if (!track.activeCues) { 

        // don't hide an already showing track.
        if (track.mode !== 'showing') { 

            // setting .mode to 'hidden' makes videojs load and parse the track.
            track.mode = 'hidden';  
        }

        // try again until track is loaded.
        window.setTimeout(function() { 
            getTrackAndDoSomething(track);
        }, 100);

    // If the track is loaded, do stuff now.
    } else {
        /* do fun stuff with the ready track here */
    }
};
```

 [1]: https://github.com/walsh9/videojs-transcript
 [2]: https://github.com/videojs/video.js/pull/1749
 [3]: http://www.w3.org/html/wg/drafts/html/master/embedded-content-0.html#dom-media-texttracks
 [4]: https://github.com/videojs/video.js/blob/fb5d0ce6ad28fe3aaeab35e0e4ce5779d75e3b4b/src/js/tracks/text-track.js#L133-137
 [5]: https://github.com/videojs/video.js/blob/14c87055306f277d5437d3a42a7178649f20206e/src/js/control-bar/text-track-controls/chapters-button.js#L56-72