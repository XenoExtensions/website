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

	let menu: HTMLDivElement;
	let burger: HTMLAnchorElement;

	function toggle() {
		menu.classList.toggle('is-active')
		burger.classList.toggle('is-active')
	}

</script>

<nav class="navbar is-dark is-fixed-top" aria-label="main navigation">
	<div class="navbar-brand">
		<a class="navbar-item" href="/">
			<img
				src="/assets/globe_1024x1024.png"
				alt="Logo"
			/>
			<p style="margin-left: 0.5rem;">XenoExtensions</p>
		</a>

		<!-- svelte-ignore a11y-missing-attribute -->
		<a
			role="button"
			class="navbar-burger"
			aria-label="menu"
			aria-expanded="false"
			bind:this={burger}
			on:click={toggle}
			on:keydown={toggle}
			tabindex="0"
		>
			<span aria-hidden="true" />
			<span aria-hidden="true" />
			<span aria-hidden="true" />
		</a>
	</div>

	<div class="navbar-menu" bind:this={menu} >
		<div class="navbar-start">

			<a class="navbar-item" href="/list"> Extensions </a>
			<a class="navbar-item" href="/donate"> Donate </a>

			<div class="navbar-item">
				<a href="https://github.com/XenoExtensions" title="GitHub" rel="nofollow noreferrer" target="_blank"><i class="fa-brands fa-github"></i></a>
			</div>

		</div>

		<div class="navbar-end">
			<a class="navbar-item" href="/disclosure"> Legal Disclosure </a>
		</div>

	</div>
</nav>

<style>
	nav a, nav a:hover {
		color: white;
	}
</style>
