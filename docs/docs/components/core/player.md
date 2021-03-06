---
title: vm-player
sidebar_label: Player
---

The root component that encapsulates all providers, plugins and UI components. This is the primary
component you will interact with to set properties on the player, listen for events and call
methods.

<!-- Auto Generated Below -->

## Usage

import Tabs from '@theme/Tabs'
import TabItem from '@theme/TabItem'

<Tabs
groupId="framework"
defaultValue="html"
values={[
  { label: 'HTML', value: 'html' },
  { label: 'React', value: 'react' },
  { label: 'Vue', value: 'vue' },
  { label: 'Svelte', value: 'svelte' },
  { label: 'Stencil', value: 'stencil' },
  { label: 'Angular', value: 'angular' }
]}>

<TabItem value="html">

```html
<vm-player controls autoplay muted current-time="30">
  <!-- Provider component is placed here. -->

  <vm-ui>
    <!-- UI components are placed here. -->
  </vm-ui>
</vm-player>

<script>
  const player = document.querySelector('vm-player');

  // Listening to an event.
  player.addEventListener('vmCurrentTimeChange', (event) => {
    const currentTime = event.detail;
    // ...
  });

  // Example function to showcase updating property.
  const seekForward = () => {
    player.currentTime += 5;
  };

  // Example function to showcase calling player method.
  const enterFullscreen = () => {
    player.enterFullscreen();
  };
</script>
```


</TabItem>

<TabItem value="react">

```tsx {2,31-43}
import React, { useState, useRef } from 'react';
import { Player, Ui } from '@vime/react';

function Example() {
  const player = useRef<HTMLVmPlayerElement>(null);
  const [currentTime, setCurrentTime] = useState(0);

  // If you prefer hooks ...
  // const [currentTime, setCurrentTime] = usePlayerContext(player, 'currentTime', 0);

  // Example function to showcase updating property.
  const seekForward = () => {
    setCurrentTime(currentTime + 5);
  };

  // Example function to showcase calling player method.
  const enterFullscreen = () => {
    player.current!.enterFulllscreen();
  };

  const onTimeUpdate = (event: CustomEvent<number>) => {
    setCurrentTime(event.detail);
  };

  const onFullscreenChange = (event: CustomEvent<boolean>) => {
    const isFullscreen = event.detail;
    // ...
  };

  return (
    <Player
      controls
      autoplay
      muted
      ref={player}
      currentTime={currentTime}
      onVmCurrentTimeChange={onTimeUpdate}
      onVmFullscreenChange={onFullscreenChange}
    >
      {/* Provider component is placed here. */}

      <Ui>{/* UI components are placed here. */}</Ui>
    </Player>
  );
}
```


</TabItem>

<TabItem value="vue">

```html {2-16,20,24-25} title="example.vue"
<template>
  <Player
    controls
    autoplay
    muted
    ref="player"
    :currentTime="currentTime"
    @vmCurrentTimeChange="onTimeUpdate"
    @vmFullscreenChange="onFullscreenChange"
  >
    <!-- Provider component is placed here. -->

    <Ui>
      <!-- UI components are placed here. -->
    </Ui>
  </Player>
</template>

<script>
  import { Player, Ui } from '@vime/vue';

  export default {
    components: {
      Player,
      Ui,
    },

    computed: {
      player() {
        return this.$refs.player;
      },
    },

    data: {
      currentTime: 0,
    },

    methods: {
      // Example function to showcase updating property.
      seekForward() {
        this.currentTime = this.currentTime + 5;
      },

      // Example function to showcase calling player method.
      enterFullscreen() {
        this.player.enterFulllscreen();
      },

      onTimeUpdate(time: number) {
        this.currentTime = time;
      },

      onFullscreenChange(active: boolean) {
        const isFullscreen = active;
        // ...
      },
    },
  };
</script>
```


</TabItem>

<TabItem value="svelte">

```tsx
<Player
  controls
  autoplay
  muted
  ref={player}
  currentTime={currentTime}
  on:vmCurrentTimeChange={onTimeUpdate}
  on:vmFullscreenChange={onFullscreenChange}
>
  <!-- Provider component is placed here. -->

  <Ui><!-- UI components are placed here. --></Ui>
</Player>
```

```html {2}
<script lang="ts">
  import { Player, Ui, usePlayerStore } from '@vime/svelte';

  let player: Player;
  let currentTime = 0;

  // OPTIONAL: If you prefer you can use the player store.
  const { paused } = usePlayerStore(player);
  $paused = false;
  $: console.log($paused);

  // Example function to showcase updating property.
  const seekForward = () => {
    currentTime += 5;
  };

  // Example function to showcase calling player method.
  const enterFullscreen = () => {
    player.enterFullscreen();
  };

  const onTimeUpdate = (event: CustomEvent<number>) => {
    currentTime = event.detail;
  };

  const onFullscreenChange = (event: CustomEvent<boolean>) => {
    const isFullscreen = event.detail;
    // ...
  };
</script>
```


</TabItem>

<TabItem value="stencil">

```tsx
import { h } from '@stencil/core';

class Example {
  private player!: HTMLVmPlayerElement;

  @State() currentTime = 0;
  
  // Example method to showcase updating property.
  private seekForward() {
    this.currentTime += 5;
  };

  // Example method to showcase calling player method.
  private enterFullscreen() {
    this.player.enterFulllscreen();
  };

  private onTimeUpdate(event: CustomEvent<number>) {
    this.currentTime = event.detail;
  };

  private onFullscreenChange(event: CustomEvent<boolean>) {
    const isFullscreen = event.detail;
    // ...
  };

  render() {
    return (
      <vm-player
        controls
        autoplay
        muted
        currentTime={this.currentTime}
        onVmCurrentTimeChange={this.onTimeUpdate.bind(this)}
        onVmFullscreenChange={this.onFullscreenChange.bind(this)}
        ref={(el) => { this.player = el; }}
      >
        {/* Provider component is placed here. */}

        <vm-ui>{/* UI components are placed here. */}</vm-ui>
      </vm-player>
    );
  }
}
```

</TabItem>

<TabItem value="angular">

```html title="example.html"
<vm-player
  #player
  autoplay
  muted
  [currentTime]="currentTime"
  (vmCurrentTimeChange)="onTimeUpdate($event)"
  (vmFullscreenChange)="onFullscreenChange($event)"
>
  <!-- Provider component is placed here. -->

  <vm-ui>
    <!-- UI components are placed here. -->
  </vm-ui>
</vm-player>
```

```ts title="example.ts"
import { ViewChild } from '@angular/core';
import { Player } from '@vime/angular';

class Example {
  @ViewChild('player') player!: Player;

  currentTime = 0;

  // Example function to showcase updating property.
  seekForward() {
    this.currentTime += 5;
  }

  // Example function to showcase calling player method.
  enterFullscreen() {
    this.player.enterFullscreen();
  }

  onTimeUpdate(event: CustomEvent<number>) {
    this.currentTime = event.detail;
  }

  onFullscreenChange(event: CustomEvent<boolean>) {
    const isFullscreen = event.detail;
    // ...
  }
}
```


</TabItem>
</Tabs>


## Properties

| Property                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Type                                                                                                                                    | Default     |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `aspectRatio`                     | The aspect ratio of the player expressed as `width:height` (`16:9`). This is only applied if the `viewType` is `video` and the player is not in fullscreen mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `string`                                                                                                                                | `'16:9'`    |
| `audioTracks` _(readonly)_        | The audio tracks associated with the current media.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | `never[]`                                                                                                                               | `[]`        |
| `autopause`                       | Whether the player should automatically pause when another Vime player starts/resumes playback.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `boolean`                                                                                                                               | `true`      |
| `autoplay`                        | Whether playback should automatically begin playing once the media is ready to do so. This will only work if the browsers `autoplay` policies have been satisfied. It'll generally work if the player is muted, or the user frequently interacts with your site. You can check if it's possible to autoplay via the `canAutoplay()` or `canMutedAutoplay()` methods. Depending on the provider, changing this prop may cause the player to completely reset.                                                                                                                                                                                                                                                                                                                                                          | `boolean`                                                                                                                               | `false`     |
| `buffered` _(readonly)_           | The length of the media in seconds that has been downloaded by the browser.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `number`                                                                                                                                | `0`         |
| `buffering` _(readonly)_          | Whether playback has temporarily stopped because of a lack of temporary data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | `boolean`                                                                                                                               | `false`     |
| `controls`                        | Indicates whether a user interface should be shown for controlling the resource. Set this to `false` when you want to provide your own custom controls, and `true` if you want the current provider to supply its own default controls. Depending on the provider, changing this prop may cause the player to completely reset.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `boolean`                                                                                                                               | `false`     |
| `currentAudioTrack` _(readonly)_  | Gets the index of the currently active audio track. Defaults to `-1` to when the default audio track is used. If you'd like to set it than see the `setCurrentAudioTrack` method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `number`                                                                                                                                | `-1`        |
| `currentPoster` _(readonly)_      | The absolute URL of the poster for the current media resource. Defaults to `undefined` if no media/poster has been loaded.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | `string ∣ undefined`                                                                                                                    | `undefined` |
| `currentProvider` _(readonly)_    | The current provider name whose responsible for loading and playing media. Defaults to `undefined` when no provider has been loaded.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `Provider.Audio ∣ Provider.Dailymotion ∣ Provider.Dash ∣ Provider.HLS ∣ Provider.Video ∣ Provider.Vimeo ∣ Provider.YouTube ∣ undefined` | `undefined` |
| `currentSrc` _(readonly)_         | The absolute URL of the media resource that has been chosen. Defaults to `undefined` if no media has been loaded.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `string ∣ undefined`                                                                                                                    | `undefined` |
| `currentTextTrack` _(readonly)_   | Gets the index of the currently active text track. Defaults to `-1` to when all text tracks are disabled. If you'd like to set it than see the `setCurrentTextTrack` method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `number`                                                                                                                                | `-1`        |
| `currentTime`                     | A `double` indicating the current playback time in seconds. Defaults to `0` if the media has not started to play and has not seeked. Setting this value seeks the media to the new time. The value can be set to a minimum of `0` and maximum of the total length of the media (indicated by the duration prop).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `number`                                                                                                                                | `0`         |
| `debug`                           | Whether the player is in debug mode and should `console.x` information about its internal state.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `boolean`                                                                                                                               | `false`     |
| `duration` _(readonly)_           | A `double` indicating the total playback length of the media in seconds. Defaults to `-1` if no media has been loaded. If the media is being streamed live then the duration is equal to `Infinity`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `number`                                                                                                                                | `-1`        |
| `i18n` _(readonly)_               | A dictionary of translations for the current language.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `Translation`                                                                                                                           | `en`        |
| `icons`                           | The default icon library to be used throughout the player. You can use a predefined icon library such as vime, material, remix or boxicons. If you'd like to provide your own see the `<vm-icon-library>` component. Remember to pass in the name of your icon library here.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `string`                                                                                                                                | `'vime'`    |
| `isAudio` _(readonly)_            | Whether the current media is of type `audio`, shorthand for `mediaType === MediaType.Audio`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `boolean`                                                                                                                               | `false`     |
| `isAudioView` _(readonly)_        | Whether the current view is of type `audio`, shorthand for `viewType === ViewType.Audio`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | `boolean`                                                                                                                               | `false`     |
| `isControlsActive`                | Whether the controls are currently visible. This is currently only supported by custom controls.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `boolean`                                                                                                                               | `false`     |
| `isFullscreenActive` _(readonly)_ | Whether the player is currently in fullscreen mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | `boolean`                                                                                                                               | `false`     |
| `isLive` _(readonly)_             | Whether the current media is being broadcast live (`duration === Infinity`).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `boolean`                                                                                                                               | `false`     |
| `isMobile` _(readonly)_           | Whether the player is in mobile mode. This is determined by parsing `window.navigator.userAgent`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `boolean`                                                                                                                               | `false`     |
| `isPiPActive` _(readonly)_        | Whether the player is currently in picture-in-picture mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `boolean`                                                                                                                               | `false`     |
| `isSettingsActive` _(readonly)_   | Whether the settings menu has been opened and is currently visible. This is currently only supported by custom settings.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | `boolean`                                                                                                                               | `false`     |
| `isTextTrackVisible` _(readonly)_ | Whether the current text tracks is visible. If you'd like to set it than see the `setTrackTrackVisibility` method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | `boolean`                                                                                                                               | `true`      |
| `isTouch` _(readonly)_            | Whether the player is in touch mode. This is determined by listening for mouse/touch events and toggling this value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `boolean`                                                                                                                               | `false`     |
| `isVideo` _(readonly)_            | Whether the current media is of type `video`, shorthand for `mediaType === MediaType.Video`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `boolean`                                                                                                                               | `false`     |
| `isVideoView` _(readonly)_        | Whether the current view is of type `video`, shorthand for `viewType === ViewType.Video`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | `boolean`                                                                                                                               | `false`     |
| `language`                        | The current language of the player. This can be any code defined via the `extendLanguage` method or the default `en`. It's recommended to use an ISO 639-1 code as that'll be used by Vime when adding new language defaults in the future.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `string`                                                                                                                                | `'en'`      |
| `languages` _(readonly)_          | The languages that are currently available. You can add new languages via the `extendLanguage` method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `string[]`                                                                                                                              | `['en']`    |
| `loop`                            | Whether media should automatically start playing from the beginning every time it ends.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `boolean`                                                                                                                               | `false`     |
| `mediaTitle` _(readonly)_         | The title of the current media. Defaults to `undefined` if no media has been loaded.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `string ∣ undefined`                                                                                                                    | `undefined` |
| `mediaType` _(readonly)_          | The type of media that is currently active, whether it's audio or video. Defaults to `undefined` when no media has been loaded or the type cannot be determined.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `MediaType.Audio ∣ MediaType.Video ∣ undefined`                                                                                         | `undefined` |
| `muted`                           | Whether the audio is muted or not.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | `boolean`                                                                                                                               | `false`     |
| `paused`                          | Whether playback should be paused. Defaults to `true` if no media has loaded or playback has not started. Setting this to `true` will begin/resume playback.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `boolean`                                                                                                                               | `true`      |
| `playbackEnded` _(readonly)_      | Whether media playback has reached the end. In other words it'll be true if `currentTime === duration`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `boolean`                                                                                                                               | `false`     |
| `playbackQualities` _(readonly)_  | The media qualities available for the current media.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `string[]`                                                                                                                              | `[]`        |
| `playbackQuality`                 | Indicates the quality of the media. The value will differ between audio and video. For audio this might be some combination of the encoding format (AAC, MP3), bitrate in kilobits per second (kbps) and sample rate in kilohertz (kHZ). For video this will be the number of vertical pixels it supports. For example, if the video has a resolution of `1920x1080` then the quality will return `1080p`. Defaults to `undefined` which you can interpret as the quality is unknown. The value can also be `Auto` for adaptive bit streams (ABR), where the provider can automatically manage the playback quality. The quality can only be set to a quality found in the `playbackQualities` prop. Some providers may not allow changing the quality, you can check if it's possible via `canSetPlaybackQuality()`. | `string ∣ undefined`                                                                                                                    | `undefined` |
| `playbackRate`                    | A `double` indicating the rate at which media is being played back. If the value is `<1` then playback is slowed down; if `>1` then playback is sped up. Defaults to `1`. The playback rate can only be set to a rate found in the `playbackRates` prop. Some providers may not allow changing the playback rate, you can check if it's possible via `canSetPlaybackRate()`.                                                                                                                                                                                                                                                                                                                                                                                                                                          | `number`                                                                                                                                | `1`         |
| `playbackRates` _(readonly)_      | The playback rates available for the current media.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | `number[]`                                                                                                                              | `[1]`       |
| `playbackReady` _(readonly)_      | Whether media is ready for playback to begin.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | `boolean`                                                                                                                               | `false`     |
| `playbackStarted` _(readonly)_    | Whether the media has initiated playback. In other words it will be true if `currentTime > 0`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `boolean`                                                                                                                               | `false`     |
| `playing` _(readonly)_            | Whether media is actively playing back. Defaults to `false` if no media has loaded or playback has not started.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `boolean`                                                                                                                               | `false`     |
| `playsinline`                     | Whether the video is to be played "inline", that is within the element's playback area. Note that setting this to false does not imply that the video will always be played in fullscreen. Depending on the provider, changing this prop may cause the player to completely reset.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | `boolean`                                                                                                                               | `false`     |
| `ready` _(readonly)_              | Whether the player has loaded and is ready to be interacted with.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `boolean`                                                                                                                               | `false`     |
| `seeking` _(readonly)_            | Whether the player is in the process of seeking to a new time position.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `boolean`                                                                                                                               | `false`     |
| `shouldRenderNativeTextTracks`    | Whether text tracks should be rendered by native player, set to `false` if using custom display.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `boolean`                                                                                                                               | `true`      |
| `textTracks` _(readonly)_         | The text tracks associated with the current media.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | `never[]`                                                                                                                               | `[]`        |
| `theme`                           | This property has no role other than scoping CSS selectors.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `string ∣ undefined`                                                                                                                    | `undefined` |
| `translations`                    | Contains each language and its respective translation map.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | `{ [x: string]: Translation; }`                                                                                                         | `{ en }`    |
| `viewType` _(readonly)_           | The type of player view that is being used, whether it's an audio player view or video player view. Normally if the media type is of audio then the view is of type audio, but in some cases it might be desirable to show a different view type. For example, when playing audio with a poster. This is subject to the provider allowing it. Defaults to `undefined` when no media has been loaded.                                                                                                                                                                                                                                                                                                                                                                                                                  | `ViewType.Audio ∣ ViewType.Video ∣ undefined`                                                                                           | `undefined` |
| `volume`                          | An `int` between `0` (silent) and `100` (loudest) indicating the audio volume.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `number`                                                                                                                                | `50`        |


## Methods

| Method                      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Signature                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `canAutoplay`               | Determines whether the player can start playback of the current media automatically.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `canAutoplay() => Promise<boolean>`                                                               |
| `canMutedAutoplay`          | Determines whether the player can start playback of the current media automatically given the player is muted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `canMutedAutoplay() => Promise<boolean>`                                                          |
| `canPlay`                   | Determines whether the current provider recognizes, and can play the given type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `canPlay(type: string) => Promise<boolean>`                                                       |
| `canSetAudioTrack`          | Returns whether the current providers allows changing the audio track.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `canSetAudioTrack() => Promise<boolean>`                                                          |
| `canSetFullscreen`          | Returns whether the native browser fullscreen API is available, or the current provider can toggle fullscreen mode. This does not mean that the operation is guaranteed to be successful, only that it can be attempted.                                                                                                                                                                                                                                                                                                                                                                                                              | `canSetFullscreen() => Promise<boolean>`                                                          |
| `canSetPiP`                 | Returns whether the current provider exposes an API for entering and exiting picture-in-picture mode. This does not mean the operation is guaranteed to be successful, only that it can be attempted.                                                                                                                                                                                                                                                                                                                                                                                                                                 | `canSetPiP() => Promise<boolean>`                                                                 |
| `canSetPlaybackQuality`     | Returns whether the current provider allows setting the `playbackQuality` prop.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `canSetPlaybackQuality() => Promise<boolean>`                                                     |
| `canSetPlaybackRate`        | Returns whether the current provider allows setting the `playbackRate` prop.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `canSetPlaybackRate() => Promise<boolean>`                                                        |
| `canSetTextTrack`           | Returns whether the current provider allows changing the text track.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `canSetTextTrack() => Promise<boolean>`                                                           |
| `canSetTextTrackVisibility` | Returns whether the current providers allows setting the text track visibility.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `canSetTextTrackVisibility() => Promise<boolean>`                                                 |
| `enterFullscreen`           | Requests to enter fullscreen mode, returning a `Promise` that will resolve if the request is made, or reject with a reason for failure. This method will first attempt to use the browsers native fullscreen API, and then fallback to requesting the provider to do it (if available). Do not rely on a resolved promise to determine if the player is in fullscreen or not. The only way to be certain is by listening to the `vmFullscreenChange` event. Some common reasons for failure are: the fullscreen API is not available, the request is made when `viewType` is audio, or the user has not interacted with the page yet. | `enterFullscreen(options?: FullscreenOptions ∣ undefined) => Promise<any>`                        |
| `enterPiP`                  | Request to enter picture-in-picture (PiP) mode, returning a `Promise` that will resolve if the request is made, or reject with a reason for failure. Do not rely on a resolved promise to determine if the player is in PiP mode or not. The only way to be certain is by listening to the `vmPiPChange` event. Some common reasons for failure are the same as the reasons for `enterFullscreen()`.                                                                                                                                                                                                                                  | `enterPiP() => Promise<void ∣ undefined>`                                                         |
| `exitFullscreen`            | Requests to exit fullscreen mode, returning a `Promise` that will resolve if the request is successful, or reject with a reason for failure. Refer to `enterFullscreen()` for more information.                                                                                                                                                                                                                                                                                                                                                                                                                                       | `exitFullscreen() => Promise<any>`                                                                |
| `exitPiP`                   | Request to exit picture-in-picture mode, returns a `Promise` that will resolve if the request is successful, or reject with a reason for failure. Refer to `enterPiP()` for more information.                                                                                                                                                                                                                                                                                                                                                                                                                                         | `exitPiP() => Promise<void ∣ undefined>`                                                          |
| `extendLanguage`            | Extends the translation map for a given language.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `extendLanguage(language: string, translation: Partial<Translation>) => Promise<void>`            |
| `getContainer`              | Returns the inner container.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `getContainer() => Promise<HTMLDivElement ∣ undefined>`                                           |
| `getProvider`               | Returns the current media provider.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | `getProvider<InternalPlayerType = any>() => Promise<AdapterHost<InternalPlayerType> ∣ undefined>` |
| `pause`                     | Pauses playback of the media.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | `pause() => Promise<void ∣ undefined>`                                                            |
| `play`                      | Begins/resumes playback of the media. If this method is called programmatically before the user has interacted with the player, the promise may be rejected subject to the browser's autoplay policies.                                                                                                                                                                                                                                                                                                                                                                                                                               | `play() => Promise<void ∣ undefined>`                                                             |
| `setCurrentAudioTrack`      | Sets the currently active audio track given the index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `setCurrentAudioTrack(trackId: number) => Promise<void>`                                          |
| `setCurrentTextTrack`       | Sets the currently active text track given the index. Set to -1 to disable all text tracks.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `setCurrentTextTrack(trackId: number) => Promise<void>`                                           |
| `setTextTrackVisibility`    | Sets the visibility of the currently active text track.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `setTextTrackVisibility(isVisible: boolean) => Promise<void>`                                     |


## Events

| Event                       | Description                                                                                                                                                                                            | Type                                                                                                                                                 |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vmAudioTracksChange`       | Emitted when the `audioTracks` prop changes value.                                                                                                                                                     | `CustomEvent<any[]>`                                                                                                                                 |
| `vmBufferedChange`          | Emitted when the `buffered` prop changes value.                                                                                                                                                        | `CustomEvent<number>`                                                                                                                                |
| `vmBufferingChange`         | Emitted when the `buffering` prop changes value.                                                                                                                                                       | `CustomEvent<boolean>`                                                                                                                               |
| `vmControlsChange`          | Emitted when the `isControlsActive` prop changes value.                                                                                                                                                | `CustomEvent<boolean>`                                                                                                                               |
| `vmCurrentAudioTrackChange` | Emitted when the `currentAudioTrack` prop changes value.                                                                                                                                               | `CustomEvent<number>`                                                                                                                                |
| `vmCurrentPosterChange`     | Emitted when the `currentPoster` prop changes value.                                                                                                                                                   | `CustomEvent<string ∣ undefined>`                                                                                                                    |
| `vmCurrentProviderChange`   | Emitted when the `currentProvider` prop changes value.                                                                                                                                                 | `CustomEvent<Provider.Audio ∣ Provider.Dailymotion ∣ Provider.Dash ∣ Provider.HLS ∣ Provider.Video ∣ Provider.Vimeo ∣ Provider.YouTube ∣ undefined>` |
| `vmCurrentSrcChange`        | Emitted when the `currentSrc` prop changes value.                                                                                                                                                      | `CustomEvent<string ∣ undefined>`                                                                                                                    |
| `vmCurrentTextTrackChange`  | Emitted when the `currentTextTrack` prop changes value.                                                                                                                                                | `CustomEvent<number>`                                                                                                                                |
| `vmCurrentTimeChange`       | Emitted when the `currentTime` prop changes value.                                                                                                                                                     | `CustomEvent<number>`                                                                                                                                |
| `vmDurationChange`          | Emitted when the `duration` prop changes value.                                                                                                                                                        | `CustomEvent<number>`                                                                                                                                |
| `vmError`                   | Emitted when an any error has occurred within the player.                                                                                                                                              | `CustomEvent<any>`                                                                                                                                   |
| `vmFullscreenChange`        | Emitted when the `isFullscreenActive` prop changes value.                                                                                                                                              | `CustomEvent<boolean>`                                                                                                                               |
| `vmI18nChange`              | Emitted when the `i18n` prop changes value.                                                                                                                                                            | `CustomEvent<Translation ∣ { [x: string]: string; }>`                                                                                                |
| `vmLanguageChange`          | Emitted when the `language` prop changes value.                                                                                                                                                        | `CustomEvent<string>`                                                                                                                                |
| `vmLanguagesChange`         | Emitted when the `languages` prop changes value.                                                                                                                                                       | `CustomEvent<string[]>`                                                                                                                              |
| `vmLiveChange`              | Emitted when the `isLive` prop changes value.                                                                                                                                                          | `CustomEvent<boolean>`                                                                                                                               |
| `vmLoadStart`               | Emitted when the provider starts loading a media resource.                                                                                                                                             | `CustomEvent<void>`                                                                                                                                  |
| `vmMediaTitleChange`        | Emitted when the `mediaTitle` prop changes value.                                                                                                                                                      | `CustomEvent<string ∣ undefined>`                                                                                                                    |
| `vmMediaTypeChange`         | Emitted when the `mediaType` prop changes value.                                                                                                                                                       | `CustomEvent<MediaType.Audio ∣ MediaType.Video ∣ undefined>`                                                                                         |
| `vmMutedChange`             | Emitted when the `muted` prop changes value.                                                                                                                                                           | `CustomEvent<boolean>`                                                                                                                               |
| `vmPausedChange`            | Emitted when the `paused` prop changes value.                                                                                                                                                          | `CustomEvent<boolean>`                                                                                                                               |
| `vmPiPChange`               | Emitted when the `isPiPActive` prop changes value.                                                                                                                                                     | `CustomEvent<boolean>`                                                                                                                               |
| `vmPlay`                    | Emitted when the media is transitioning from `paused` to `playing`. Event flow: `paused` -> `play` -> `playing`. The media starts `playing` once enough content has buffered to begin/resume playback. | `CustomEvent<void>`                                                                                                                                  |
| `vmPlaybackEnded`           | Emitted when playback reaches the end of the media.                                                                                                                                                    | `CustomEvent<void>`                                                                                                                                  |
| `vmPlaybackQualitiesChange` | Emitted when the `playbackQualities` prop changes value.                                                                                                                                               | `CustomEvent<string[]>`                                                                                                                              |
| `vmPlaybackQualityChange`   | Emitted when the `playbackQuality` prop changes value.                                                                                                                                                 | `CustomEvent<string ∣ undefined>`                                                                                                                    |
| `vmPlaybackRateChange`      | Emitted when the `playbackRate` prop changes value.                                                                                                                                                    | `CustomEvent<number>`                                                                                                                                |
| `vmPlaybackRatesChange`     | Emitted when the `playbackRates` prop changes value.                                                                                                                                                   | `CustomEvent<number[]>`                                                                                                                              |
| `vmPlaybackReady`           | Emitted when the media is ready to begin playback. The following props are guaranteed to be defined when this fires: `mediaTitle`, `currentSrc`, `currentPoster`, `duration`, `mediaType`, `viewType`. | `CustomEvent<void>`                                                                                                                                  |
| `vmPlaybackStarted`         | Emitted when the media initiates playback.                                                                                                                                                             | `CustomEvent<void>`                                                                                                                                  |
| `vmPlayingChange`           | Emitted when the `playing` prop changes value.                                                                                                                                                         | `CustomEvent<boolean>`                                                                                                                               |
| `vmReady`                   | Emitted when the player has loaded and is ready to be interacted with.                                                                                                                                 | `CustomEvent<void>`                                                                                                                                  |
| `vmSeeked`                  | Emitted directly after the player has successfully transitioned/seeked to a new time position. Event flow: `seeking` -> `seeked`.                                                                      | `CustomEvent<void>`                                                                                                                                  |
| `vmSeekingChange`           | Emitted when the `seeking` prop changes value.                                                                                                                                                         | `CustomEvent<boolean>`                                                                                                                               |
| `vmTextTracksChange`        | Emitted when the `textTracks` prop changes value.                                                                                                                                                      | `CustomEvent<TextTrack[]>`                                                                                                                           |
| `vmTextTrackVisibleChange`  | Emitted when the `isTextTrackVisible` prop changes value.                                                                                                                                              | `CustomEvent<boolean>`                                                                                                                               |
| `vmThemeChange`             | Emitted when the `theme` prop changes value.                                                                                                                                                           | `CustomEvent<string ∣ undefined>`                                                                                                                    |
| `vmTouchChange`             | Emitted when the `isTouch` prop changes value.                                                                                                                                                         | `CustomEvent<boolean>`                                                                                                                               |
| `vmTranslationsChange`      | Emitted when the `translations` prop changes value.                                                                                                                                                    | `CustomEvent<{ [x: string]: Translation; }>`                                                                                                         |
| `vmViewTypeChange`          | Emitted when the `viewType` prop changes value.                                                                                                                                                        | `CustomEvent<ViewType.Audio ∣ ViewType.Video ∣ undefined>`                                                                                           |
| `vmVolumeChange`            | Emitted when the `volume` prop changes value.                                                                                                                                                          | `CustomEvent<number>`                                                                                                                                |


## Slots

| Slot | Description                                           |
| ---- | ----------------------------------------------------- |
|      | Used to pass in providers, plugins and UI components. |


## CSS Custom Properties

| Name                        | Description                                                                                                                |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `--vm-blocker-z-index`      | The blocker's position in the root z-axis stack inside the player.                                                         |
| `--vm-player-bg`            | The background color of the player, has no effect on audio players.                                                        |
| `--vm-player-border-radius` | The border radius of the player.                                                                                           |
| `--vm-player-box-shadow`    | The shadow cast around the player frame.                                                                                   |
| `--vm-player-font-family`   | A custom font family to be used throughout the player.                                                                     |
| `--vm-player-theme`         | A custom theme (color) to be used throughout the player. Any valid CSS `color` property (HEX, RGBA, HLS, ...) can be used. |


