<script setup>
	import { RouterLink, RouterView } from 'vue-router';
	import { ref, reactive, onMounted } from 'vue';

	const url = ref('');
	const token = ref('');
	const isRegisterView = ref(false);

	const baseURL = window.location.origin;
	url.value = new URL(location.href);

	const handleLogout = () => {
		localStorage.removeItem('token');
		window.open('/', '_self');
	};

	onMounted(() => {
		if (url.value.href === 'http://localhost:3000/register')
			isRegisterView.value = true;

		token.value = localStorage.getItem('token');
	});
</script>
<template>
	<nav
		class="navbar"
		role="navigation"
		aria-label="main navigation"
		v-if="!isRegisterView"
	>
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
					<button class="button is-info is-outlined">
						Create new Asset
					</button>
					<button class="button is-info is-outlined">
						Show all Asset
					</button>
					<button class="button is-info is-outlined">
						Search for an Asset
					</button>
				</div>
			</div>

			<div class="navbar-end">
				<div class="navbar-item">
					<div class="buttons">
						<!-- <a class="button is-light"> Log in </a> -->
						<a
							href="/register"
							class="button is-primary"
							v-if="!token"
							>Log in</a
						>
						<a @click="handleLogout" class="button is-warning" v-else
							>Log out</a
						>
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
	@import '../node_modules/bulma/css/bulma.min.css';
</style>
