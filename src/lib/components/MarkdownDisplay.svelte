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

	export let url: string;

	let md: string;

	onMount(() => {

		// Prevent potential XSS issues. No idea how this could be exploited, but safety first I guess.
		if(!url.startsWith('/')) url = '/' + url

		fetch(url).then(async (res) => {
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
	});

</script>

{#if md}
	<div class="markdown">
		{@html md}
	</div>
{/if}

<style>
	.markdown {
		margin-bottom: 3rem;
	}
</style>