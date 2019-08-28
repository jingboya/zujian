<template>
	<ul class="nav nav-pills nav-justified step" :class="[className]">
		<li class="nav-item" v-for="(name,index) in names" :class="{'active': index <= step }" :key="index">
			<a class="nav-link" v-if="!!next" @click="select(index)">{{name}}</a>
			<a class="nav-link" v-else>{{name}}</a>
		</li>
	</ul>
</template>
<script>
	export default {
		props: {
			names: Array,
			current: {
				type:Number,
				default:1
			},
			theme: {
				type:String,
				default:'round'
			},
			next: {
				type:Boolean,
				default:false
			}
		},
		data() {
			return {
				step: 1,
				maps: {
					progress: 'step-progress',
					round: 'step-round',
					square: 'step-square',
					arrow: 'step-arrow'
				}
			}
		},
		computed: {
			className() {
				return this.maps[this.theme]
			}
		},
		watch:{
			current(v){
				this.step = v - 1
			}
		},
		methods: {
			select(idx) {
				this.step = idx + 1
			},
			setStep(){
				this.step = typeof this.current != undefined ? this.current - 1 : 1
			}
		},
		mounted() {
			this.step = typeof this.current != undefined ? this.current - 1 : 1
		}
	}
</script>
<style lang="less">
	@import (reference) "../../assets/lib/css.less";
	@import "../../assets/lib/step.less";
</style>