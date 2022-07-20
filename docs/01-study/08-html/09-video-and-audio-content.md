---
layout: default
title: Video and audio content
parent: HTML
grand_parent: Study
nav_order: 9
mathjax: true
mermaid: true
permalink: /docs/html/9
---

# Video and audio content
{: .no_toc }

<details markdown="block">
  <summary>
	Table of contents
  </summary>
{: .fs-3 .text-delta }
- TOC
{:toc}
</details>

---

> 참고: [Video and audio content](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)

- Objective: To learn how to embed video and audio content into a webpage, and add captions/subtitles to video

## Video and audio on the web

- In the early days, native web technologies such as HTML didn't have the ability to embed video and audio on the Web, so proprietary (or plugin-based) technologies like Flash became popular for handling such content

- This kind of technology worked OK, but it had a number of problems, including not working well with HTML/CSS features, security issues, and accessibility issues

- a few years later the HTML5 specification had such features added, with the `<video>` and `<audio>` element, and some new JavaScript APIs for controlling them

> Note
>
> Before you begin here, you should also know that there are quite a few OVPs (online video providers) like YouTube, and online audio providers like Soundcloud. Such companies offer a convenient, easy way to host and consume videos, so you don't have to worry about the enormous bandwidth consumption. OVPs even usually offer ready-made code for embedding video/audio in your webpages

### The `<video>` element

- The `<video>` element allows you to embed a video very easily

```html
<video src="rabbit320.webm" controls>
  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.webm">link to the video</a> instead.</p>
</video>
```

##### features of note

- `src`

	- the `src` (source) attribute contains a path to the video you want to embed

- `controls`

	- Users must be able to control video and audio playback

	- You must either use the controls attribute to include the browser's own control interface, or build your interface using the appropriat JavaScript API

	- At a minimum, the interface must include a way to start and stop the media, and adjust the volume

- The paragraph inside the `<video>` tags

	- This is called fallback content $---$ this will be displayed if the browser accessing the page doesn't support the `<video>` element, allowing us to provide a fallback for older browsers

### Using multiple source formats to improve compatibility

- If you've tried to access with an olde browser, the video won't play, because different browsers support different video (and audio) formats

- There are things you can do to help prevent this from being a problem

##### Contents of a media file

- Formats like MP3, MP4 and WebM are called container formats

- They define a structure in which the audio and/or video tracks that make up the media are stored, along with metadata describing the media, what codecs are used to encode its channels, and so forth

- The audio and video tracks within the container hold data in the appropriate format for the codec used to encode that media

- Different formats are used for audio tracks versus video traks

- Each audio track is encoded using an audio codec, while video tracks are encoded uwing a video codec

- Different browser support different video and audio formats, and different container formats

	- A WebM container typically packages Vorbis or Opus audio with VP8/VP9 video. This is supported in all modern browsers, ghough older versions may not work

	- An MP4 containeroften packages AAC or MP3 audio with H.264 video. this is also supported in all modern browsers, as well as Internet Explorer

	- The Ogg container tends to use Vorbis audio and Theora video. This is best supported in Firefox and Chrome, but has basically been superseded by the better quality WebM format

- There are some special cases. For example, for some types of audio, a codec's data is often stored without a container, or with a simplifies container.

- One such instance is the FLAC codec, which is stored most commonly in FLAC files, which are just raw FLAC tracks

- Another such situation is MP3 file. An MP3 file is actually an MPEG-1 Audio Layer 3 (MP3) audio track stored whithin an MPEG or MPEG-2 container

- This is especially interesint since while most browsers don't support using MPEG media in the `<video>` and `<audio>` elements, they may still support MP3 due to its popularity

- An audio player will tend to play an audio track directly,e.g. an MP3 or Ogg file. These don't need containers

##### Media file support in browsers

> Note
>
> Why do we have this problem? It turns out that several popular formats, such as MP3 and MP4/H.264, are excellent but are encumbered by patents. In the United States, patents covered MP3 until 2017, and H.264 is encumbered by patents through at least 2027
>
> Because of those patents, browsers that wish to implement support for those codecs must pay typically enormous license fees

- The codecs exist to compress video and audio into manageable files, since raw audio and video are both exceedingly large

- Each web browser supports an assortment of codecs, like Vorbis or H.264, which are used to convert the compressed audio and video int obinary data and back

- Each codec offers its own advantages and drawbacks, adn each container may also offerits own positive and negative features affecting your decisions about which to use

- Thins become slightly more complicated because not only does each browser support a different set of container file formats, they also each support a different selection of codecs

- In order to maximize the likelihood that your web site or app will sork on a user's browser, you may need to provide each media file you use in multiple formats

- Due to the intricacies of ensuring your app's media is viewable across every combination of browsers, platforms and devices you wish to reach, choosing the best combination of codecs and container can be a complicated task

- Mobile browsers may support additional formats not supported by their desktop equivalents, just like they may not support all the same formats the descktop version does

- On top of that, both desktop and mobile browsers may be designed to offload handling of media playback (either for all media or only for specific types it can't handle internally)

- This means media support is parly dependent on what software the user has installed

- So how do we do this?

```html
<video controls>
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
</video>
```

- We've taken the `src` attribute out of the actual `<video>` tag, and instead included separate `<source>` elements that point to their own sources

- In this case the browser will go through the `<source>` elements and play the first one that it has the codec to support

- Including WebM and MP4 sources should be enough to play your video on most platforms and browsers these days

- Each `<source>` element also has a `type` attribute

- This is optional, but it is advised that you include it

- The `type` attribute contains the MIME type of the file specified by the `<source>`, and browsers can use the `type` to immediately skip videos they don't understand

### Other `<video>` features

```html
<video controls width="400" height="400"
       autoplay loop muted preload="auto"
       poster="poster.png">
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>Your browser doesn't support HTML video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
</video>
```

##### Features

- `width` and `height`

	- You can control the video size either with these attributes or with CSS

	- In both cases, videos maintain their native widthfheight ratio $---$ known as the aspect ratio

- `autoplay`

	- Makes the audio or video start playing right away, while the rest of the page is loading

	- You are advised not to use autoplaying video (or audio) on your sites, because users can find it really annoying

- `loop`

	- Makes the video (or audio) start playing again whenever it finishes

	- this can also be annoying, so only use if really necessary

- `muted`

	- Causes the media to play with the sound turned off by default

- `poster`

	- The URL of an image which will be displayed before the video is played, It is intended to be used for a splash screen or advertising screen

- `preload`

	- Used for buffering large files; it can take one of three values

		- `"none"`: does not buffer the file

		- `"auto"`: buffers the media file

		- `"metadata"` buffers only the metadata for the file

### the <audio> element

```html
<audio controls>
  <source src="viper.mp3" type="audio/mp3">
  <source src="viper.ogg" type="audio/ogg">
  <p>Your browser doesn't support HTML5 audio. Here is a <a href="viper.mp3">link to the audio</a> instead.</p>
</audio>
```

- This takes up less space than a video player, as there is no visual component

- The `<audio>` elment doesn't support the `width`/`height` attributes

- It also doesn't support the `poster` attribute

- Other than this, `<audio>` supports all the same features as `<video>`

## Displaying video text tracks

- Wouldn't it be nice to be able to provide with a transcript of the words being spoken in the audio/video?

- To do so we use the WebVTT file format and the `<track>` elment

> Note
>
> "Transcrib" means "to write down spoken words as text". The resulting text is a "transcript"

- WebVTT is a format for writing text files containing multiple strings of text along with metadata such as the time in the video at which each text string should be displayed, and even limited styling/positioning information

- These text strings are called cues, and there are several kinds of cues which are ued for different purposes

##### The most Common cues

- Subtitles

	- Translations of foreing material for people who don't understand the words spoken in the audio

- Captions

	- Synchronized transcriptions of dialog or descriptions of significant sounds to let people who can'tt head the audio understand whatis going on

- Timed descriptions

	- Text which should be spoken by the media player in order to describe important visuals to blind or otherwise visually impaired users

##### How to apply

- A typical WebVTT file

```WEBVTT
1
00:00:22.230 --> 00:00:24.606
This is the first subtitle.

2
00:00:30.739 --> 00:00:34.074
This is the second.

…
```

1. Save it as a `.vtt` file in a sensible place

2. Linke to the `.vtt` file with the `<track>` element. `<track>` should be placed within `<audio>` or `<video>`, but after all `<source>` elements

	- Use the `kind` attribute to specify whether the cues are `subtitles`, `captions`, or `descriptions`

	- Further, use `srclang` to tell the browser what language you have written the subtitles in

	- Finally, add `label` to help readers identify the language they are searching for

- here's an example

```html
<video controls>
    <source src="example.mp4" type="video/mp4">
    <source src="example.webm" type="video/webm">
    <track kind="subtitles" src="subtitles_es.vtt" srclang="es" label="Spanish">
</video>
```

> Note
>
> Text tracks also help you with SEO, since search engines especially thrive on text. Text tracks even allow search engines to link directly to a spot partway through the video

- You may have to do some conversion, but there are enough programs out there to allow you to do this without too much trouble, such as [Miro Video Converter](http://www.mirovideoconverter.com/) and [Audacity](http://www.mirovideoconverter.com/)
