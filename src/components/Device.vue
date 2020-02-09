<template>
	<div class="device" v-bind:class="{ 'is-online': device.online }">
		<div class="grid-item">{{ isOnline(device) }}</div>
		<div class="grid-item display-name">{{ device.display_name }}</div>
		<div class="grid-item">
			{{
				device.latest_device_point.lat.toFixed(2) +
					", " +
					device.latest_device_point.lng.toFixed(2)
			}}
		</div>
		<div>{{convertDate(device.latest_device_point.dt_tracker)}}</div>
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
		},
		convertDate(dateStr) {
			const secDiff = (new Date() - new Date(dateStr)) / 1000

			if(secDiff < 60) {
				return `${secDiff.toFixed(0)} sec`
			}
			else if(secDiff < 3600) {
				return `${(secDiff/60).toFixed(0)} min`
			}
			else if(secDiff < 86400) {
				return `${(secDiff/3600).toFixed(0)} hr`
			}
			else  {
				return `${(secDiff/86400).toFixed(0)} day`
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
	grid-template-columns: repeat(4, 1fr);
}

.is-online {
	background: #54b2f9;
}
.grid-item {
	text-align: center;
	padding: 6px;
}
.display-name{
	text-align:left;
}
</style>
