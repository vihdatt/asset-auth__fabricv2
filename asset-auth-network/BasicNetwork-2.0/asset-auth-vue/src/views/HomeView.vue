<script setup>
	import APIClient from '../api/APIClient';
	import { ref, reactive, onBeforeMount, computed } from 'vue';

	const assets = ref(null);
	const isLoading = ref(false);

	const d = new Date();

	const registerDate = computed(() => {
		console.log(assets.value);
	});

	const getDateXDaysAgo = (numOfDays, d) => {
		const daysAgo = d.getTime();
	};

	const handleQueryAllAsset = async () => {
		APIClient.queryAllAsset().then(async (rs) => {
			assets.value = await rs.data;
		});
	};

	const handleLastUpdateDate = (timeString) => {
		if (timeString.length > 10) return 'Long';
		return 'okay';
	};

	onBeforeMount(async () => {
		await handleQueryAllAsset();
		isLoading.value = true;
	});
</script>

<template v-if="isLoading">
	<div class="table-container">
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
			<tbody v-for="(asset, index) in assets" :key="index">
				<td>{{ asset.Key }}</td>
				<td>{{ asset.Record.manufacturer }}</td>
				<td>{{ asset.Record.name }}</td>
				<td>{{ asset.Record.serialnumber }}</td>
				<td>{{ asset.Record.ownerid }}</td>
				<td>{{ asset.Record.ownername }}</td>
				<td>{{ asset.Record.registerdate }}</td>
				<td>
					{{ handleLastUpdateDate(asset.Record.lastupdatedate) }}
				</td>
				<td>
					<div class="buttons">
						<button class="button is-info">Edit</button>
						<button class="button is-success">History</button>
						<button class="button is-danger">Delete</button>
					</div>
				</td>
			</tbody>
		</table>
	</div>
</template>
