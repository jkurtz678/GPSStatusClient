<template>
	<div class="container">
		<Loading
			:active.sync="waitingForResponse"
			:is-full-page="false"
			:opacity="0.6"
		/>
		<div class="column-headers" v-if="devices.length !== 0">
			<button
				class="can-click"
				v-bind:class="{ 'sorting-by': column_sort === 'status' }"
				@click="columnHeaderClicked('status')"
			>
				Status
			</button>
			<button
				class="can-click"
				v-bind:class="{ 'sorting-by': column_sort === 'name' }"
				@click="columnHeaderClicked('name')"
			>
				Display Name
			</button>
			<button>Latest Point</button>
			<button
				class="can-click"
				v-bind:class="{ 'sorting-by': column_sort === 'age' }"
				@click="columnHeaderClicked('age')"
			>
				Updated Time
			</button>
		</div>
		<div
			v-for="device in sortDevices(devices)"
			v-bind:key="device.factory_id"
		>
			<Device v-bind:device="device" />
		</div>
	</div>
</template>

<script>
import Device from "./Device.vue";
import "vue-loading-overlay/dist/vue-loading.css";
import Loading from "vue-loading-overlay";

export default {
	name: "DevicesContainer",
	components: {
		Device,
		Loading
	},
	props: ["devices", "waitingForResponse"],
	data() {
		return {
			column_sort: null
		};
	},
	methods: {
		//sorts devices based on selected column
		sortDevices(devices) {
			const sortDevices = devices.slice();
			if (this.column_sort === "status") {
				sortDevices.sort((a, b) => (a.online < b.online ? 1 : -1));
			} else if (this.column_sort === "name") {
				sortDevices.sort((a, b) =>
					a.display_name > b.display_name ? 1 : -1
				);
			} else if (this.column_sort === "age") {
				sortDevices.sort((a, b) =>
					a.latest_device_point.dt_tracker <
					b.latest_device_point.dt_tracker
						? 1
						: -1
				);
			}
			return sortDevices;
		},
		//toggle column header selected
		columnHeaderClicked(column) {
			if (column === this.column_sort) {
				this.column_sort = null;
			} else {
				this.column_sort = column;
			}
		}
	}
};
</script>

<style scoped>
.container {
	margin-left: 15%;
	margin-right: 15%;
	position: relative;
	min-height: 500px;
}

button {
	text-decoration: underline;
	margin-bottom: 0px;
	font-size: 1.3em;
	margin: 0px 6px 5px 6px;
	background-color: transparent;
	outline: none;
	border: none;
	font-weight: bold;
}

.sorting-by {
	background-color: #094079;
	color: white;
}

.column-headers {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	padding: 3px;
}
</style>
