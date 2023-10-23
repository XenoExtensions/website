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
	import { goto } from '$app/navigation';

	export let extension: Extension;
</script>

<div
	class="card has-background-dark"
	role="button"
	tabindex="0"
	on:click={() => goto(`/list/${extension.id}`)}
	on:keypress={() => goto(`/list/${extension.id}`)}
>
	<div class="card-image">
		<figure class="image is-4by3">
			<img src={`/logos/${extension.id}.png`} alt="Logo" style="object-fit: contain;">
		</figure>
	</div>
	<div class="card-content">
		<p class="card-title has-text-white">{extension.name}</p>

		<div class="content has-text-white">
			{extension.description}
		</div>
	</div>
</div>

<style>
	.card {
		margin: 1rem;
		width: 300px; /* Adjust as needed */
		display: flex;
		flex-direction: column;
		cursor: pointer;
	}

	.card-title {
		font-size: 1.25rem;
		max-width: 100%; /* Allow the title to expand */
		overflow: hidden;
		white-space: nowrap; /* Prevent line breaks */
		text-overflow: ellipsis; /* Show ellipsis (...) if text overflows */
	}

	.card-image {
		padding: 1rem;
	}
</style>
