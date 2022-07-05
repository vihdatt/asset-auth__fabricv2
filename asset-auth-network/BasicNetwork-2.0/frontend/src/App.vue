<script setup>
	import { RouterLink, RouterView } from 'vue-router';
</script>

<template>
	<nav class="navbar" role="navigation" aria-label="main navigation">
		<div class="navbar-brand">
			<a class="navbar-item" href="/">
				<h1 class="is-size-4 mr-6">AssetAuth</h1>
			</a>

			<a
				role="button"
				class="navbar-burger"
				aria-label="menu"
				aria-expanded="false"
				data-target="navbarBasicExample"
			>
				<span aria-hidden="true"></span>
				<span aria-hidden="true"></span>
				<span aria-hidden="true"></span>
			</a>
		</div>

		<div id="navbarBasicExample" class="navbar-menu">
			<div class="navbar-start ml-6">
				<div class="buttons are-normal">
					<button class="button">Create new Asset</button>
					<button class="button">Show all Asset</button>
					<button class="button">Search for an Asset</button>
				</div>
			</div>

			<div class="navbar-end">
				<div class="navbar-item">
					<div class="buttons">
						<a class="button is-primary">
							<strong>Sign up</strong>
						</a>
						<a class="button is-light"> Log in </a>
					</div>
				</div>
			</div>
		</div>
	</nav>

	<section>
		<RouterView />
	</section>
</template>

<style>
	/* @import '@/assets/base.css'; */
	@import '../node_modules/bulma/css/bulma.min.css';
</style>
