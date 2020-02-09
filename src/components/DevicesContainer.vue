<template>
	<div class="container">
		<div class="column-headers">
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

export default {
	name: "DevicesContainer",
	components: {
		Device
	},
	props: ["devices"]
};
</script>

<style scoped>
.container {
	margin-left: 20%;
	margin-right: 20%;
	
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
