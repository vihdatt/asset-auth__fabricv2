<script setup>
	import APIClient from '../api/APIClient';
	import { ref, reactive } from 'vue';

	const emit = defineEmits(['closeSearchAnAssetModal']);

	const assetKey = ref('');

	const handleSubmit = () => {
		console.log(assetKey.value);
		if (assetKey.value.trim() != '') {
			APIClient.queryAnAsset({
				args: `["${assetKey.value}"]`,
				peer: 'peer0.gov.assetauth.vn',
				fcn: 'queryAsset',
			}).then((rs) => {
				if (rs.data.error !== 'undefine') {
					const searchAsset = rs.data;
					console.log(searchAsset);
					emit('closeSearchAnAssetModal');
				}
			});
		}
	};
</script>

<template>
	<div class="modal is-active">
		<div class="modal-background"></div>
		<div class="modal-content">
			<div class="container">
				<h1 class="title has-text-centered">Search for an Asset</h1>

				<div class="field">
					<label class="label">Asset Key</label>
					<div class="control">
						<input
							class="input"
							type="text"
							placeholder="Asset Key"
							v-model="assetKey"
						/>
					</div>
				</div>

				<div class="field is-grouped mt-5">
					<div class="control">
						<button class="button is-link" @click="handleSubmit">
							Search
						</button>
					</div>
					<div class="control">
						<button
							class="button is-link is-light"
							@click="$emit('closeSearchAnAssetModal')"
						>
							Cancel
						</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<style scoped>
	.container {
		padding: 3rem 2rem;
		background-color: white;
		border-radius: 1rem;
	}
</style>
