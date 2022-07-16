<script setup>
	import APIClient from '../api/APIClient';
	import { ref, reactive, onBeforeMount, computed } from 'vue';

	const assets = ref(null);
	const isLoading = ref(false);
	const searchInput = ref('');

	const filteredAssets = computed(() => {
		if (searchInput.value === '') return assets.value;
		else {
			return assets.value.filter((asset) => {
				return asset.Key.includes(searchInput.value);
			});
		}
	});

	const d = new Date();

	const registerDate = computed(() => {
		console.log(assets.value);
	});

	const getDateXDaysAgo = (numOfDays, d) => {
		const daysAgo = d.getTime();
	};

	const handleQueryAllAsset = async () => {
		APIClient.queryAllAsset().then(async (rs) => {
			assets.value = await rs.data.filter((item) => {
				return !item.Record.isdelete;
			});
		});
	};

	const handleLastUpdateDate = (timeString) => {
		if (timeString.length > 10) return 'Long';
		return 'okay';
	};

	const handleDelete = (assetKey) => {
		console.log(assetKey);
		APIClient.deleteAnAsset({
			args: [assetKey],
		}).then((rs) => {
			if (rs.data.error == null) {
				alert(`Delete asset ${assetKey} successfully!`);
				reloadPage();
			} else {
				alert('Delete failed!');
			}
		});
	};

	const reloadPage = () => {
		window.open('/', '_self');
	};

	onBeforeMount(async () => {
		await handleQueryAllAsset();
		isLoading.value = true;
	});
</script>

<template v-if="isLoading">
	<div class="table-container">
		<div class="field has-addons search-bar">
			<div class="control">
				<input
					class="input"
					type="text"
					placeholder="Search for an asset"
					v-model="searchInput"
				/>
			</div>
			<p v-if="!filteredAssets.length" class="alert has-text-danger">
				Can not find that asset!
			</p>
		</div>

		<table
			class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth"
		>
			<thead>
				<tr>
					<th>Key</th>
					<th>Manufacturer</th>
					<th>Name</th>
					<th>Serial number</th>
					<th>Owner ID</th>
					<th>Owner name</th>
					<th>Register date</th>
					<th>Last update date</th>
					<th></th>
				</tr>
			</thead>
			<tbody v-for="(asset, index) in filteredAssets" :key="index">
				<td>{{ asset.Key }}</td>
				<td>{{ asset.Record.manufacturer }}</td>
				<td>{{ asset.Record.name }}</td>
				<td>{{ asset.Record.serialnumber }}</td>
				<td>{{ asset.Record.ownerid }}</td>
				<td>{{ asset.Record.ownername }}</td>
				<td>{{ asset.Record.registerdate.slice(0, 10) }}</td>
				<td>
					{{ asset.Record.lastupdatedate.slice(0, 10) }}
				</td>
				<td>
					<div class="buttons">
						<button class="button is-info">Edit</button>
						<button class="button is-success">History</button>
						<button
							class="button is-danger"
							@click="handleDelete(asset.Key)"
						>
							Delete
						</button>
					</div>
				</td>
			</tbody>
		</table>
	</div>
</template>

<style scoped>
	.search-bar {
		margin-left: 14.2rem;
	}
	.alert {
		margin: auto 0.8rem;
	}
</style>
