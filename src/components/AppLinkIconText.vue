<template>
	<a  v-if="typeItem === 'link'" href="#" :class="{active:currentPage !== '' && currentPage===pageName}" class="focus:(outline-none shadow-focus) hover:bg-gray-100 flex flex-grow items-center px-[2.4rem] text-base ">
		<slot name="icon">
			<mdicon v-if="icon !== ''" :name="getIcon" :width="iconSize.width" :height="iconSize.height" class="mr-[2.4rem]">
			</mdicon>
		</slot>
		<slot></slot>
	</a>

	<button v-if="typeItem === 'button'" :class="{active:currentPage !== '' && currentPage===pageName}" class="focus:(outline-none shadow-focus) hover:bg-gray-100 flex flex-grow items-center px-[2.4rem] text-base ">
		<slot name="icon">
			<mdicon v-if="icon !== ''" :name="icon" :width="iconSize.width" :height="iconSize.height" class="mr-[2.4rem]">
			</mdicon>
		</slot>
		<slot></slot>
	</button>

</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
	props: {
		icon: {
			type: String,
			default: '',
		},
		iconSize: {
			type: Object,
			default: {width: 24, height: 24}
		},
		currentPage: {
			type: String,
		},
		pageName: {
			type: String,
			default: ''
		}, 
		iconExeption: {
			type: Array,
			default: []
		},
		typeItem: {
			type: String,
			default: 'link'
		}
	},
	computed: {
		getIcon() {
			if (this.iconExeption.includes(this.icon)){
				return this.icon
			} else if (this.currentPage !== this.pageName){
				const res = this.icon + '-outline'
				return res
			} else {
				return this.icon
			}
		}
	}
})
</script>

<style>
.active{
	@apply bg-gray-50 font-medium;
}
</style>