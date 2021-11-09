<template>
	<li class="flex h-[4rem]">
		<AppLinkIconText :typeItem="typeItem" :iconExeption="iconExeption" :iconSize="iconSize" :icon="icon" :currentPage="currentPage" :pageName="pageName">
			<slot name="icon"></slot>
			<slot></slot>
		</AppLinkIconText>
	</li>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import AppLinkIconText from './AppLinkIconText.vue'

export default defineComponent({
	props: {
		icon: {
			type: String,
			default: ''
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
			default: '',
		},
		typeItem: {
			type: String,
		},
	},
	data() {
		return {
			iconExeption: ['broadcast', 'playlist-play']
		}
	},
	components: {
		AppLinkIconText,
		
	}
})
</script>