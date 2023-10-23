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
	import hjson from 'hjson'
    import { onMount } from 'svelte';
	import ExtensionCard from '$lib/components/ExtensionCard.svelte';

	let extensions: Extension[] = []

	onMount(() => {
		fetch('/extensions.hjson')
			.then(async data => {
				let raw = <Extension[]> hjson.parse(await data.text())
				raw.sort((a, b) => {
					if(a.id > b.id){
						return 1
					} else {
						return -1
					}
				})
				extensions = raw
			})
	})

</script>

<div class="container has-text-centered">
	<h1>Extension List</h1>

	<div class="card-container" style="margin-bottom: 2rem;">
		{#each extensions as extension}
			<ExtensionCard {extension} />
		{/each}
	</div>
</div>

<svelte:head>
	<title>Extension List | XenoExtensions</title>
</svelte:head>

<style>
	.card-container {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}
</style>