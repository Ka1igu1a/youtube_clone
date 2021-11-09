<template>
<div class="container flex flex-col w-[24rem] overflow-y-auto overflow-x-hidden h-full " tabindex="-1">
	<ul class="btn__group">
		<HeaderMenuVerticalItem icon="home-variant" pageName="main" :currentPage="currentPage">
			Главная
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="compass" pageName="feed" :currentPage="currentPage">
			Навигатор
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="pencil-box-multiple" pageName="subscriptions" :currentPage="currentPage">
			Подписки
		</HeaderMenuVerticalItem>
	</ul>

	<hr class="divider">

	<ul class="btn__group">
		<HeaderMenuVerticalItem icon="play-box-multiple" pageName="lib" :currentPage="currentPage">
			Библиотека
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="archive-clock" pageName="history" :currentPage="currentPage">
			История
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="play-box" pageName="myvideos" :currentPage="currentPage">
			Ваши видео
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="clock-time-five" pageName="later" :currentPage="currentPage">
			Смотреть позже
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="thumb-up" pageName="liked" :currentPage="currentPage">
			Понравившиеся
		</HeaderMenuVerticalItem>

		<template v-if="isUserPlaylistsOpen">
			<HeaderMenuVerticalItem v-for="(playlist, i) in userData.playlists" :key="i" icon="playlist-play">
				{{playlist}}
			</HeaderMenuVerticalItem>
		</template>

		<HeaderMenuVerticalItem 
		v-if="userData.playlists.length > 0" 
		@click="isUserPlaylistsOpen = !isUserPlaylistsOpen"
		:icon="getExpandIcon(isUserPlaylistsOpen)" 
		typeItem="button">
			{{isUserPlaylistsOpen ? 'Свернуть' : 'Развернуть'}}
		</HeaderMenuVerticalItem>
	</ul>

	<hr class="divider">

	<div class="btn__group">
		<span class="subttile">Подписки</span>
		<ul v-if="userData.subscriptions.length > 0" >
			<template v-for="(chanel, i) in userData.subscriptions" :key="i">
				<HeaderMenuVerticalItem v-if="i < 7" :currentPage="currentPage">
					<template v-slot:icon>
						<img src="../assets/avatar.jpg" alt="Аватар пользовотеля" class="rounded-full w-[2.4rem] mr-[2.4rem]">
					</template>
					{{chanel}}
				</HeaderMenuVerticalItem>
			</template>
			<template v-for="(chanel, i) in userData.subscriptions" :key="i">
				<HeaderMenuVerticalItem v-if="isUserSubscriptionsOpen && i >= 7" :currentPage="currentPage">
					<template v-slot:icon>
						<img src="../assets/avatar.jpg" alt="Аватар пользовотеля" class="rounded-full w-[2.4rem] mr-[2.4rem]">
					</template>
					{{chanel}}
				</HeaderMenuVerticalItem>
			</template>
			<HeaderMenuVerticalItem v-if="userData.subscriptions.length > 7" :icon="getExpandIcon(isUserSubscriptionsOpen)" 
				@click="isUserSubscriptionsOpen = !isUserSubscriptionsOpen" typeItem="button">
				{{isUserSubscriptionsOpen ? 'Свернуть' : 'Показать еще ' + String(userData.subscriptions.length - 7)}}
			</HeaderMenuVerticalItem>
		</ul>
		<span v-else class="text-base text-gray-500 px-[2.4rem] py-[.8rem]">У вас пока нет подписок</span>
	</div>
	<hr class="divider">

	<div class="btn__group">
		<span class="subttile">Другие возможности</span>
		<ul>
			<HeaderMenuVerticalItem icon="crown" pageName="" :currentPage="currentPage">
				YouTube Premium
			</HeaderMenuVerticalItem>
			<HeaderMenuVerticalItem icon="movie-open" pageName="" :currentPage="currentPage">
				Фильмы
			</HeaderMenuVerticalItem>
			<HeaderMenuVerticalItem icon="controller-classic" pageName="" :currentPage="currentPage">
				Видеоигры
			</HeaderMenuVerticalItem>
			<HeaderMenuVerticalItem icon="broadcast" pageName="broadcast" :currentPage="currentPage">
				Трансляции
			</HeaderMenuVerticalItem>
			<HeaderMenuVerticalItem icon="thumb-up" pageName="" :currentPage="currentPage">
				Спорт
			</HeaderMenuVerticalItem>
		</ul>
	</div>
	<hr class="divider">

	<ul class="btn__group">
		<HeaderMenuVerticalItem icon="cog" pageName="" :currentPage="currentPage">
			Настройки
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="flag" pageName="" :currentPage="currentPage">
			Жалобы
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="help-circle" pageName="" :currentPage="currentPage">
			Справка
		</HeaderMenuVerticalItem>
		<HeaderMenuVerticalItem icon="comment-alert" pageName="" :currentPage="currentPage">
			Отправить отзыв
		</HeaderMenuVerticalItem>
	</ul>
	<hr class="divider">
	<div class="btn__group flex flex-col px-[2.4rem] whitespace-nowrap ">
		<div v-for="(block, i) in [
			['О сервисе', 'Прессе', 'Авторские права', 'Связаться с нами','Авторам', 'Рекламодателям', 'Разработчикам'],
			['Условия использования', 'Конфиденциальность', 'Правила и безопасность', 'Как работает YouTube','Тестирование новых функций']]"
			:key="i" class="flex flex-wrap text-s text-gray-500 font-medium mb-[.8rem]">
			<a href="#" 
			class="mr-[.5rem]"
			v-for="(title, i) in block"
			:key="i">
				{{title}}
			</a>
		</div>
		<span class="text-s text-gray-500">© 2021 Google LLC</span>
	</div>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HeaderMenuVerticalItem from './HeaderMenuVerticalItem.vue'

export default defineComponent({
	props: {
		userData: {
			type: Object,
			default: {}
		},
		currentPage: {
			type: String,
			default: ''
		}
	},
	data() {
		return {
			isUserPlaylistsOpen: false,
			isUserSubscriptionsOpen: false,
		}
	},
	components: {
		HeaderMenuVerticalItem
	},
	methods: {
		getExpandIcon(state) {
			return state ? 'chevron-up' : 'chevron-down'
		}
	},
})
</script>

<style scoped lang="scss">
	.divider{
		@apply text-gray-50 ;
	}
	.subttile{
		@apply inline-block text-base text-gray-500 uppercase px-[2.4rem] py-[.8rem] font-medium;
	}
	.container{
		scrollbar-width: thin;
		scrollbar-color: gray white;
	}
	.btn__group{
		@apply py-[.8rem]
	}
</style>