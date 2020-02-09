<template>
	<div class="container">
		<Loading
			:active.sync="waitingForResponse"
			:is-full-page="false"
			:opacity="0.6"
		/>
		<div class="column-headers" v-if="devices.length !== 0">
			<h3>Status</h3>
			<h3>Display Name</h3>
			<h3>Latest point</h3>
		</div>
		<div v-for="device in devices" v-bind:key="device.factory_id">
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
	props: ["devices", "waitingForResponse"]
};
</script>

<style scoped>
.container {
	margin-left: 20%;
	margin-right: 20%;
	position: relative;
	min-height: 500px;
}

h3 {
	text-decoration: underline;
	margin-bottom: 0px;
}

.column-headers {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	padding: 10px;
}
</style>
