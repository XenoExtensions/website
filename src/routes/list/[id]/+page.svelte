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

<script lang="ts">
	import { onMount } from "svelte";
	import hjson from "hjson";
	import MarkdownDisplay from "$lib/components/MarkdownDisplay.svelte";

	export let data;

	let extension: Extension | undefined;

	onMount(() => {
		fetch('/extensions.hjson')
			.then(async res => {
				const jsonData = <Extension[]> hjson.parse(await res.text())
				extension = jsonData.find(x => {
					return x.id == data.id
				})
			})
	});
</script>

<div class="container has-text-centered">
	<img src={`/logos/${data.id}.png`} alt="Logo" id="logo" />
	<MarkdownDisplay url={`/pages/${data.id}.md`} />
</div>

<svelte:head>
	<title>{extension?.name} | XenoExtensions</title>
</svelte:head>

<style>
	#logo {
		width: 10rem;
	}
</style>
