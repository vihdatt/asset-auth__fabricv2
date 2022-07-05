<script setup>
	import { ref, reactive } from 'vue';
	import APIClient from '../api/APIClient';
	const user = ref('');
	const org = ref('');

	const onSubmit = () => {
		APIClient.getTokenRegister({
			orgName: org.value,
			username: user.value,
		}).then((rs) => {
			if (rs.status === 200) {
				localStorage.setItem('token', rs.data.token);
				window.open('/', '_self');
			}
		});
	};
</script>

<template>
	<section class="hero is-primary is-fullheight">
		<div class="hero-body">
			<div class="container">
				<div class="columns is-centered">
					<div
						class="column is-5-tablet is-4-desktop is-3-widescreen"
					>
						<form @submit.prevent="onSubmit" class="box">
							<div class="field">
								<label for="" class="label">UserName</label>
								<div class="control has-icons-left">
									<input class="input" v-model="user" required />
									<span class="icon is-small is-left">
										<i class="fa fa-envelope"></i>
									</span>
								</div>
							</div>
							<div class="field">
								<label for="" class="label">Organization</label>
								<div class="control has-icons-left">
									<input class="input" v-model="org" required />
									<span class="icon is-small is-left">
										<i class="fa fa-lock"></i>
									</span>
								</div>
							</div>
							<div class="field has-text-centered">
								<button type="submit" class="button is-success">
									Login
								</button>
							</div>
						</form>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>

<style></style>
