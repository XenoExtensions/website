<!--
 Copyright (C) 2023 Marcus Huber (xenorio) <dev@xenorio.xyz>
 
 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU Affero General Public License as
 published by the Free Software Foundation, either version 3 of the
 License, or (at your option) any later version.
 
 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU Affero General Public License for more details.
 
 You should have received a copy of the GNU Affero General Public License
 along with this program.  If not, see <http://www.gnu.org/licenses/>.
-->

# TubeTweaks
## Various enhancements for YouTube

---

### Current Features
- Prevent generating/loading trackable share links <span style="color: red;">(Load prevention only available on Firefox)</span>
- Change hostname of share links from youtu.be to www.youtube.com

---

### Note to Chrome/Chromium users

Due to Google's [ManifestV3 shenanigans](https://youtu.be/8KWCLhHrblE?t=206), functionality of this extension is severely limited on chromium-based browsers. 

TubeTweaks needs to intercept and modify network requests to work properly (similar to an ad blocker), which is no longer possible on Chromium.

Where possible, workarounds are implemented in the Chromium version. However, these may feel rather clunky. 

Where no workarounds are possible, the respective feature is removed.

If you want to use TubeTweaks to its full extent, please consider switching to Firefox!

---

### Download

<a href="https://addons.mozilla.org/en-US/firefox/addon/tubetweaks/" rel="nofollow noreferrer" target="_blank">
	<button class="button is-warning"><i class="fa-brands fa-firefox-browser"></i> Firefox</button>
</a>


<a href="#" rel="nofollow noreferrer" target="_blank">
	<button class="button is-warning" disabled><i class="fa-brands fa-chrome"></i> Chromium (Coming Soon)</button>
</a>
 

<a href="https://github.com/XenoExtensions/TubeTweaks" rel="nofollow noreferrer" target="_blank">
	<button class="button is-warning"><i class="fa-brands fa-github"></i> Source Code</button>
</a>


