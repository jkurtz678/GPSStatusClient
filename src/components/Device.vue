<template>
	<div class="device" v-bind:class="{ 'is-online': device.online }">
		<div class="grid-item">{{ isOnline(device) }}</div>
		<div class="grid-item">{{ device.display_name }}</div>
		<div class="grid-item">
			{{
				device.latest_device_point.lat.toFixed(2) +
					", " +
					device.latest_device_point.lng.toFixed(2)
			}}
		</div>
	</div>
</template>

<script>
export default {
	name: "Device",
	props: ["device"],
	methods: {
		isOnline(device) {
			if(device.online) {
				return "Online"
			}
			else {
				return "Offline"
			} 
		}
	}
};
</script>

<style scoped>
.device {
	background: #f4f4f4;
	border-bottom: 1px #ccc dotted;
	padding: 10px;
	display: grid;
	grid-template-columns: repeat(3, 1fr);
}

.is-online {
	background: #94fccd;
}
.grid-item {
	text-align: center;
	padding: 6px;
}
</style>
