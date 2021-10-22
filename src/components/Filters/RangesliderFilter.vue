<template>
	<div>
		<svg :id="sliderid + 'hist'" style="width: 100%;height: 50px;margin-bottom: 1em;" ref="hist">
			<rect v-for="(h, i) in hist" :x="i * histBarWidth + '%'" :y="(1 - h.value / histMax) * 100 +'%'" :width="histBarWidth + '%'" :height="h.value / histMax * 100 +'%'" class="inrange" :data-bucket="h.key" :data-bucket-obs="h.value" v-bind:key="h.key"></rect>
		</svg>
		
		<div :id="sliderid" ref="slider"></div>
		<div style="margin-top: 5em;">
			<input :id="sliderid + 'min'" class="min" type="number" for="number" step="1" :min="list.min" :max="list.max" @change="textboxchange" ref="min" :value="list.min" />
			<input :id="sliderid + 'max'" class="max" type="number" for="number" step="1" :min="list.min" :max="list.max" @change="textboxchange" ref="max" :value="list.max"/>
			<input :id="sliderid + 'reset'" type="button" value="Reset" @click="sliderreset" ref="reset" />
		</div>
	</div>
</template>

<script>
	export default {
		props:  ['list', 'sliderid', 'hist', 'pips'],
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
				this.$refs.select.value = -1;
			}
		},
		computed: {
			histMax(){
				return Math.max(...this.hist.map(e=>e.value))
			},
			histBarWidth(){
				return (1 / this.hist.length * 100) 
			}
		}
	}
</script>

<!--
<style type="text/css" src="https://cdn.jsdelivr.net/gh/orchidjs/tom-select@1.7.5/dist/css/tom-select.bootstrap5.min.css"></style>
-->
<style scoped>

</style>
