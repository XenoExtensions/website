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
	import rehypeStringify from "rehype-stringify";
	import remarkParse from "remark-parse";
	import remarkRehype from "remark-rehype";
	import rehypeExternalLinks from "rehype-external-links";
	import { unified } from "unified";
	import hjson from "hjson";

	export let data;

	let extension: Extension | undefined;
	let md: string;

	onMount(() => {
		fetch(`/pages/${data.id}.md`).then(async (res) => {
			md = String(
				// We do not sanitize HTML here, as input is static. Do not blindly copy this into other projects!
				await unified()
					.use(remarkParse)
					.use(remarkRehype, { allowDangerousHtml: true })
					.use(rehypeExternalLinks, {
						rel: ["noreferrer", "nofollow"],
						target: "_blank",
					})
					.use(rehypeStringify, { allowDangerousHtml: true })
					.process(await res.text())
			);
		});

		fetch('/extensions.hjson')
			.then(async res => {
				const jsonData = <Extension[]> hjson.parse(await res.text())
				extension = jsonData.find(x => {
					return x.id == data.id
				})
			})
	});
</script>

{#if md}
	<div class="container has-text-centered markdown">
		<img src={`/logos/${data.id}.png`} alt="Logo" id="logo" />
		{@html md}
	</div>
{/if}

<svelte:head>
	<title>{extension?.name} | XenoExtensions</title>
</svelte:head>

<style>
	#logo {
		width: 10rem;
	}
	.markdown {
		margin-bottom: 3rem;
	}
</style>
