<template>
	<header>
		<nav role="navigation">
			<!-- Horizontal menu -->
			<div class="flex px-[1.6rem] items-center justify-between sticky top-0 w-full bg-[#FFF] z-50" role="menubar">
				<!-- Logo & Menu button -->
				<div class="flex">
					<!-- Menu button -->
					<button class="self-center p-[.8rem] rounded-full
					 focus:(outline-none shadow-focus)
					 active:(bg-gray-100)"
					 role="button"
					 aria-label="Toggle menu"
					 @click="isMenuOpen = !isMenuOpen">
						<mdicon name="menu" :width="24" :height="24"/>
					</button>
					<!-- Logo -->
					<div class="flex px-[1.6rem] py-[1.8rem] whitespace-nowrap self-center" role="banner">
						<a href="#" alt="Main page Youtube" aria-label="Go to main page" role="link" class="focus:(outline-none shadow-focus)">
							<img src="../assets/youtube-logo.png" alt="Logo Youtube" title="Главная страница Youtube" class="inline-block min-w-[9rem] h-[2rem] ">
						</a>
						<sup class="text-xs text-gray-500 ml-[.5rem] ">{{counryCode}}</sup>
					</div>
				</div>

				<!-- Search -->
				<div role="search" class="flex items-center max-w-[70rem] w-full h-[4rem] justify-center items-stretch">
					<form class="flex-grow" action="#">
						<div class="flex">
							<div class="flex border-1 border-gray-100 rounded-l-sm px-[.4rem] 
							focus-within:(border-blue-accent shadow-inner) flex-grow justify-between"> 
								<!-- Input -->
								<input type="text" placeholder="Введите запрос" class="text-xl flex-grow h-[4rem] focus:(outline-none)">
								<!-- Keyboard button -->
								<button type="button" role="button" aria-label="Open screen keyboard" class="mr-[.8rem] self-center p-[.4rem] 
								focus:(outline-none shadow-focus) opacity-50 hover:opacity-100">
									<mdicon name="keyboard" :width="24" :height="24" />
								</button>
							</div>
							<!-- Search button -->
							<div class="flex border-1 border-gray-100 border-l-0 rounded-r-sm focus-within:(bg-gray-100)">
								<button type="submit" role="button" aria-label="search" data-tooltip="Введите запрос" class="focus:(outline-none) px-[1.6rem] hover:(bg-gray-50)">
									<mdicon name="magnify" :width="24" :height="24" />	
								</button>
							</div>
						</div>
					</form>
					<div class="flex ml-[.8rem]">
						<button role="button" class="p-[.8rem] rounded-full focus:(outline-none shadow-focus)
						 active:(bg-gray-100 rounded-full)">
							<mdicon name="microphone" :width="24" :height="24" />
						</button>
					</div>
				</div>

				<!-- Right bar -->
				<div class="flex">
					<div class="flex space-x-3">
						<button class="btn__icon" data-tooltip="Создать">
							<mdicon name="video-plus-outline" :width="24" :height="24" ></mdicon>
						</button>
						<button class="btn__icon" data-tooltip="Приложения Youtube">
							<mdicon name="dots-grid" :width="24" :height="24" ></mdicon>
						</button>
						<button class="btn__icon" data-tooltip="Уведомления">
							<mdicon name="bell-ring-outline" :width="24" :height="24" ></mdicon>
						</button>
					</div>
					<button class="btn__icon profile ml-[1.8rem] ">
						<img src="../assets/avatar.jpg" alt="Аватар пользовотеля" class="rounded-full">
					</button>
				</div>
			</div>

			<!-- Vertical menu -->
			<HeaderMenuVertical v-if="isMenuOpen" :userData="userData" :currentPage="currentPage" class="fixed" role="menu"/>
			<div v-else class=" fixed">
				<a href="#" class="flex flex-col py-[1.6rem] px-[.8rem] items-center hover:(bg-gray-50)">
					<mdicon :name="'home-variant'" class="mb-[.4rem]"></mdicon>
					Главная
				</a>
				<a href="#" class="flex flex-col py-[1.6rem] px-[.8rem] items-center hover:(bg-gray-50)">
					<mdicon :name="'compass'" class="mb-[.4rem]"></mdicon>
					Навигатор
				</a>
				<a href="#" class="flex flex-col py-[1.6rem] px-[.8rem] items-center hover:(bg-gray-50)">
					<mdicon :name="'pencil-box-multiple'" class="mb-[.4rem]"></mdicon>
					Подписки
				</a>
				<a href="#" class="flex flex-col py-[1.6rem] px-[.8rem] items-center hover:(bg-gray-50)">
					<mdicon :name="'play-box-multiple'" class="mb-[.4rem]"></mdicon>
					Библиотека
				</a>
			</div>
		</nav>
	</header>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HeaderMenuVertical from './HeaderMenuVertical.vue'

export default defineComponent({
	components: {
		HeaderMenuVertical
	},
	data() {
		return {
			counryCode: 'RU',
			currentPage: 'feed',
			isMenuOpen: true,
			userData: {
				playlists: ['Nginx', 'Git'],
				subscriptions: ['Мы обречены', 'Vadim Makeev', 'Мы обречены', 'Vadim Makeev', 'Мы обречены', 'Vadim Makeev', 'Мы обречены', 'Vadim Makeev',
				'Google', 'Firefox']
			}
		}
	}
})
</script>

<style scoped lang="scss">
[data-tooltip]{
	position: relative;
}
[data-tooltip]::after {
    content: attr(data-tooltip);
    @apply absolute rounded left-0 top-full bg-gray-500 whitespace-nowrap p-[1rem]
    text-[#FFF] pointer-events-none opacity-0 transition-all duration-300 text-m;
}	
[data-tooltip]:hover::after {
  @apply opacity-70;
  top: calc(100% + .5rem);
}
.btn__icon{
	@apply rounded-full focus:(outline-none shadow-focus) w-[4rem] h-[4rem]
}
.profile{
	@apply focus:(shadow-focusAccent)
}
</style>