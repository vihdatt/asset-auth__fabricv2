<script setup>
	import APIClient from '../api/APIClient';
	import { ref, reactive } from 'vue';

	const emit = defineEmits(['handleShowCreateNewAssetModel']);

	const asset = reactive({
		key: '',
		manufacturer: '',
		name: '',
		serialNumber: '',
		ownerID: '',
		ownerName: '',
	});

	const handleSubmit = () => {
		console.log(asset.key);
		if (
			asset.key.trim() != '' &&
			asset.manufacturer.trim() != '' &&
			asset.name.trim() != '' &&
			asset.serialNumber.trim() != '' &&
			asset.ownerID.trim() != '' &&
			asset.ownerName.trim() != ''
		) {
			APIClient.createAnAsset({
				args: [
					asset.key,
					asset.manufacturer,
					asset.name,
					asset.serialNumber,
					asset.ownerID,
					asset.ownerName,
				],
			}).then((rs) => {
				console.log(rs);
				if (rs.data.error == null) {
					alert('Create successfully!');
					window.open('/', '_self');
				} else {
					alert('Create failed!');
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
				<h1 class="title has-text-centered">Create New Asset</h1>

				<div class="field">
					<label class="label">Key</label>
					<div class="control">
						<input
							class="input"
							type="text"
							placeholder="Asset Key"
							v-model="asset.key"
						/>
					</div>
				</div>

				<div class="field">
					<label class="label">Manufacturer</label>
					<div class="control">
						<div class="select">
							<select v-model="asset.manufacturer">
								<option>Car</option>
								<option>Motorbike</option>
							</select>
						</div>
					</div>
				</div>

				<div class="field">
					<label class="label">Name</label>
					<div class="control">
						<input
							class="input"
							type="text"
							placeholder="Asset Name"
							v-model="asset.name"
						/>
					</div>
				</div>

				<div class="field">
					<label class="label">Serial Number</label>
					<div class="control">
						<input
							class="input"
							type="text"
							placeholder="Serial Number"
							v-model="asset.serialNumber"
						/>
					</div>
				</div>

				<div class="field">
					<label class="label">Owner ID</label>
					<div class="control">
						<input
							class="input"
							type="text"
							placeholder="Owner ID"
							v-model="asset.ownerID"
						/>
					</div>
				</div>

				<div class="field">
					<label class="label">Owner Name</label>
					<div class="control">
						<input
							class="input"
							type="text"
							placeholder="Owner Name"
							v-model="asset.ownerName"
						/>
					</div>
				</div>

				<div class="field is-grouped mt-5">
					<div class="control">
						<button class="button is-link" @click="handleSubmit">
							Create
						</button>
					</div>
					<div class="control">
						<button
							class="button is-link is-light"
							@click="$emit('closeCreateNewAssetModal')"
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
