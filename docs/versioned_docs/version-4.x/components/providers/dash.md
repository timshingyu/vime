---
title: vime-dash
sidebar_label: Dash
---

import Tabs from '@theme/Tabs'
import TabItem from '@theme/TabItem'

Enables loading, playing and controlling [MPEG DASH](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP)
based media. It uses [`dashjs`](https://github.com/Dash-Industry-Forum/dash.js.md) under the hood.

> You don't interact with this component for passing player properties, controlling playback, listening to player events and so on, that is all done through the `vime-player` component.

<!-- Auto Generated Below -->

## Usage

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

```html {2-6}
<vime-player controls>
  <vime-dash
    src="/media/manifest.mpd"
    version="latest"
    poster="/media/poster.png"
  ></vime-dash>
  <!-- ... -->
</vime-player>
```

</TabItem>


<TabItem value="react">

```tsx {2,14-19}
import React from 'react';
import { VimePlayer, VimeDash } from '@vime/react';

function Example() {
  /**
   * @see https://github.com/Dash-Industry-Forum/dash.js.
   */
  const dashConfig = {
    // ...
  };

  return (
    <VimePlayer controls>
      <VimeDash
        src="/media/manifest.mpd"
        version="latest"
        config={dashConfig}
        poster="/media/poster.png"
      />
      {/* ... */}
    </VimePlayer>
  );
}
```

</TabItem>


<TabItem value="vue">

```html {3-8,14,19} title="example.vue"
<template>
  <VimePlayer controls>
    <VimeDash
      src="/media/manifest.mpd"
      :config="dashConfig"
      version="latest"
      poster="/media/poster.png"
    />
    <!-- ... -->
  </VimePlayer>
</template>

<script>
  import { VimePlayer, VimeDash } from '@vime/vue';

  export default {
    components: {
      VimePlayer,
      VimeDash,
    },

    data: {
      /**
       * @see https://github.com/Dash-Industry-Forum/dash.js.
       */
      dashConfig: {
        // ...
      },
    },
  };
</script>
```

</TabItem>


<TabItem value="svelte">

```html {2-7,12} title="example.svelte"
<VimePlayer controls>
  <VimeDash
    src="/media/manifest.mpd"
    version="latest"
    config="{dashConfig}"
    poster="/media/poster.png"
  />
  <!-- ... -->
</VimePlayer>

<script lang="ts">
  import { VimePlayer, VimeDash } from '@vime/svelte';

  /**
   * @see https://github.com/Dash-Industry-Forum/dash.js.
   */
  const dashConfig = {
    // ...
  };
</script>
```

</TabItem>


<TabItem value="stencil">

```tsx {5-9}
class Example {
  render() {
    return (
      <vime-player controls>
        <vime-dash
          src="/media/manifest.mpd"
          version="latest"
          poster="/media/poster.png"
        />
        {/* ... */}
      </vime-player>
    );
  }
}
```

</TabItem>


<TabItem value="angular">

```html {2-7} title="example.html"
<vime-player controls>
  <vime-dash
    [config]="dashConfig"
    src="/media/manifest.mpd"
    version="latest"
    poster="/media/poster.png"
  ></vime-dash>
  <!-- ... -->
</vime-player>
```

```ts title="example.ts"
class Example {
  /**
   * @see https://github.com/Dash-Industry-Forum/dash.js.
   */
  dashConfig = {
    // ...
  };
}
```

</TabItem>
    
</Tabs>


## Properties

| Property                | Attribute                 | Description                                                                                                                                                                                                                                                                        | Type                                               | Default      |
| ----------------------- | ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- | ------------ |
| `autoPiP`               | `auto-pip`                | **EXPERIMENTAL:** Whether the browser should automatically toggle picture-in-picture mode as the user switches back and forth between this document and another document or application.                                                                                           | `boolean ∣ undefined`                              | `undefined`  |
| `config`                | --                        | The `dashjs` configuration.                                                                                                                                                                                                                                                        | `{ [x: string]: any; }`                            | `{}`         |
| `controlsList`          | `controls-list`           | Determines what controls to show on the media element whenever the browser shows its own set of controls (e.g. when the controls attribute is specified).                                                                                                                          | `string ∣ undefined`                               | `undefined`  |
| `crossOrigin`           | `cross-origin`            | Whether to use CORS to fetch the related image. See [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin) for more information.                                                                                                                          | `"" ∣ "anonymous" ∣ "use-credentials" ∣ undefined` | `undefined`  |
| `disablePiP`            | `disable-pip`             | **EXPERIMENTAL:** Prevents the browser from suggesting a picture-in-picture context menu or to request picture-in-picture automatically in some cases.                                                                                                                             | `boolean ∣ undefined`                              | `undefined`  |
| `disableRemotePlayback` | `disable-remote-playback` | **EXPERIMENTAL:** Whether to disable the capability of remote playback in devices that are attached using wired (HDMI, DVI, etc.) and wireless technologies (Miracast, Chromecast, DLNA, AirPlay, etc).                                                                            | `boolean ∣ undefined`                              | `undefined`  |
| `mediaTitle`            | `media-title`             | The title of the current media.                                                                                                                                                                                                                                                    | `string ∣ undefined`                               | `undefined`  |
| `poster`                | `poster`                  | A URL for an image to be shown while the video is downloading. If this attribute isn't specified, nothing is displayed until the first frame is available, then the first frame is shown as the poster frame.                                                                      | `string ∣ undefined`                               | `undefined`  |
| `preload`               | `preload`                 | Provides a hint to the browser about what the author thinks will lead to the best user experience with regards to what content is loaded before the video is played. See [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video#attr-preload) for more information. | `"" ∣ "auto" ∣ "metadata" ∣ "none" ∣ undefined`    | `'metadata'` |
| `src` _(required)_      | `src`                     | The URL of the `manifest.mpd` file to use.                                                                                                                                                                                                                                         | `string`                                           | `undefined`  |
| `version`               | `version`                 | The NPM package version of the `dashjs` library to download and use.                                                                                                                                                                                                               | `string`                                           | `'latest'`   |

## Dependencies

### Used by

- [vime-playground](../core/playground.md)

### Depends on

- [vime-video](video.md)

### Graph

```mermaid
graph TD;
  vime-dash --> vime-video
  vime-video --> vime-file
  vime-playground --> vime-dash
  style vime-dash fill:#f9f,stroke:#333,stroke-width:4px
```

---

_Built with [StencilJS](https://stenciljs.com/)_
