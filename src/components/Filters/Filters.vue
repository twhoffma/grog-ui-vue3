<template>
	<div v-if="list">
		<label for="boardgamedesigner">Boardgamedesigner</label>
		<DropdownFilter dropdownid="boardgamedesigner" :list="list.boardgamedesigner" ref="boardgamedesigner" />
		
		<label for="boardgameartist">Boardgameartist</label>
		<DropdownFilter dropdownid="boardgameartist" :list="list.boardgameartist" ref="boardgameartist" />
		
		<label for="boardgamepublisher">Boardgamepublisher</label>
		<DropdownFilter dropdownid="boardgamepublisher" :list="list.boardgamepublisher" ref="boardgamepublisher" />
		
		<label for="boardgamemechanic">Boardgamemechanic</label>
		<DropdownFilter dropdownid="boardgamemechanic" :list="list.boardgamemechanic" ref="boardgamemechanic" />
		
		<label for="boardgamecategory">Boardgamecategory</label>
		<DropdownFilter dropdownid="boardgamecategory" :list="list.boardgamecategory" ref="boardgamecategory" />
		
		<label for="boardgamefamily">Boardgamefamily</label>
		<DropdownFilter dropdownid="boardgamefamily" :list="list.boardgamefamily" ref="boardgamefamily" />

		<label for="playtime">Playtime</label>
		<RangesliderFilter sliderid="playtime" :list="list.playtime" :hist="list.playtimehist" ref="playtime" />
		
		<label for="numplayers">Num players</label>
		<RangesliderFilter sliderid="numplayers" :list="list.numplayers" :hist="list.numplayershist" pips="true" ref="numplayers" />
		
		<label for="playtime">Year published</label>
		<RangesliderFilter sliderid="yearpublished" :list="list.yearpublished" :hist="list.yearpublishedhist" pips="true" ref="yearpublished" />
 
	</div>
</template>

<script>
	import DropdownFilter from '@/components/Filters/DropdownFilter.vue'
	import RangesliderFilter from '@/components/Filters/RangesliderFilter.vue'
	
	export default {
		//name: "Filters",
		components: {
			'DropdownFilter': DropdownFilter,
			'RangesliderFilter': RangesliderFilter
		},
		created: function(){
		console.log("Created!");
		
		let url = "staticdata/filters-275399.json";
		//var list;
		
		var vm = this;
			
		fetch(url).then(function(r){
			if(r.ok){
				//console.log(r);
				//list = JSON.parse(r);
				//list = r.json();
				r.json().then(function(list){
					list.yearpublished = {
						min: Math.min(...list.yearpublished.map(e => parseInt(e))),
						max: Math.max(...list.yearpublished.map(e => parseInt(e)))
					}
					
					vm.list = list;
				});
			}else{
				console.log("Fetch not OK!");
			}
			
			console.log(r);
			console.log("fetch returned!");
		}).catch(function(e){
			console.log("Fetch failed! " + e)
		});
		
		
		//this.list = list;
	},
	data: function(){
		var list = null; //Vue.observable({});
		
		return {
			list: list,
			loading: true
		}
	},
	mounted: function () {
		console.log("Mounted app!");
		this.$nextTick(function () {
			//console.log("Mounted tick!");
		});
	},
	methods: {
		appendFilter(arg, event){
			console.log("Appended!" + event);
			//Should append or overwrite this part of the query
		},
		applyFilter(arg, event){
			console.log("Applied filter!" + event);
			
			/* 
				var filter = {
					'boardgamedesigner': this.$refs.boardgamedesigner.$refs.select.value,
					'boardgameartist': this.$refs.boardgameartist.$refs.select.value,
					'boardgamepublisher': this.$refs.boardgamepublisher.$refs.select.value,
					'boardgamemechanic': this.$refs.boardgamemechanic.$refs.select.value,
					'boardgamecategory': this.$refs.boardgamecategory.$refs.select.value,
					'boardgamefamily': this.$refs.boardgamefamily.$refs.select.value,
					'yearpublished': [
						this.$refs.yearpublished.$refs.min.value, 
						this.$refs.yearpublished.$refs.max.value
					],
					'numplayers': [
						this.$refs.numplayers.$refs.min.value, 
						this.$refs.numplayers.$refs.max.value
					],
					'playtime': [
						this.$refs.playtime.$refs.min.value, 
						this.$refs.playtime.$refs.max.value
					]
				}; 
	     			console.log(filter);
				*/
			}
		}
	}
</script>

<style scoped>

</style>
