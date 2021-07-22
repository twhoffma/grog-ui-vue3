<template>
	<div>
		<select :id="dropdownid" placeholder="All" autocomplete="off" ref="select">
			<option value="-1">All</option>
			<option v-for="item in list" :value="item.objectid" v-bind:key="item.objectid">{{item.name}}</option>
		</select>

		<input :id="dropdownid + 'reset'" type="button" value="Reset" @click="resetdropdown" />
	</div>
</template>

<script>
	export default {
		//name: 'DropdownFilter',
		props: ['list', 'dropdownid'],
		mounted: function(){
			console.log("Component " + this.dropdownid + " mounted!");
			//var id = this.dropdownid;
			
			/* 
			var t = new window.TomSelect("#" + this.dropdownid, {
				create: false,
				sortField: {
					field: "text",
					direction: "asc"
				}
			});
			*/
			//Not sure if this is good form..
			//this.tomSelect = t;
			//We need query to match value to select    
		},
		updated: function(){
			console.log("Component updated!");
		},
		methods: {
			resetdropdown(){
				console.log("Reset dropdown!");
				//this.tomSelect.setValue("All");
			}
		}
	}
</script>

<!--
<style type="text/css" src="https://cdn.jsdelivr.net/gh/orchidjs/tom-select@1.7.5/dist/css/tom-select.bootstrap5.min.css"></style>
-->
<style scoped>

</style>
