<template>
	<div class="drawer">
		<input id="my-drawer" type="checkbox" class="drawer-toggle"/>
		<div class="drawer-content flex flex-col">
			<!-- Navbar -->
			<div class="navbar bg-base-300 w-full z-30 sticky top-0">
				<div class="flex-none lg:hidden">
					<label for="my-drawer" aria-label="open sidebar" class="btn btn-square btn-ghost">
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							class="inline-block h-6 w-6 stroke-current">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M4 6h16M4 12h16M4 18h16"></path>
						</svg>
					</label>
				</div>
				<NuxtLink class="mx-2 flex-1 px-2" href="/"><span class="font-bold text-accent text-2xl">CUII</span><span class="text-2xl">Liste.de</span></NuxtLink>
				<div class="hidden flex-none lg:block">
					<ul class="menu menu-horizontal">
						<li v-for="page in pages" :key="page.name">
							<MenuItem :link="page.link" :active="currentPage === page.link" :icon="page.icon" :class="page.hide_if_small ? 'hidden xl:block' : ''">
								{{ page.name }}
							</MenuItem>
						</li>
					</ul>
				</div>
			</div>
			<section class="mt-4 mx-4 xl:mx-16">
				<slot></slot>
			</section>
		</div>
		<div class="drawer-side">
			<label for="my-drawer" aria-label="close sidebar" class="drawer-overlay"></label>
			<ul class="menu bg-base-200 min-h-full w-80 p-4">
				<li v-for="page in pages" :key="page.name">
					<MenuItem :link="page.link" :active="currentPage === page.link">
						<Icon :name="page.icon" class="mr-2" :class="{ 'text-accent': currentPage === page.link }" />
						{{ page.name }}
					</MenuItem>
				</li>
			</ul>
		</div>
	</div>
</template>

<script setup>

let pages = [
	{name: 'Home', link: '/', icon: 'iconamoon:home-fill', hide_if_small: true},
	{name: 'Gesperrte Domains', link: '/domains', icon: 'iconamoon:search'},
	{name: 'Domain hinzufügen', link: '/probe', icon: 'tabler:plus'},
	{name: 'Bin ich betroffen?', link: '/isp', icon: 'pepicons-pop:question'},
	{name: 'Zensur umgehen', link: '/umgehen', icon: 'mdi:shield-check'},
	{name: 'Über uns', link: '/about', icon: 'mdi:information-outline'},
]

const route = useRoute()

const currentPage = ref("/")
currentPage.value = route.path

// on route change, update currentPage
watch(() => route.path, (newVal) => {
	currentPage.value = newVal
})


definePageMeta({
	middleware: ['old-cuiiliste-redirects'],
})

useSeoMeta({
	title: 'CUII Liste',
	ogTitle: 'CuiiListe.de',
	description: 'Die CUII Liste zeigt dir, welche Domains von der CUII gesperrt sind und wie du die Zensur umgehen kannst.',
	ogDescription: 'Die CUII Liste zeigt dir, welche Domains von der CUII gesperrt sind und wie du die Zensur umgehen kannst.',
	ogImage: '/img/nocuii.png',
	ogUrl: 'https://cuiiliste.de',
	twitterTitle: 'CuiiListe.de',
	twitterImage: '/img/nocuii.png',
	twitterCard: 'summary',
	twitterDescription: 'Die CUII Liste zeigt dir, welche Domains von der CUII gesperrt sind und wie du die Zensur umgehen kannst.',
	themeColor: '#f26e24'
})
useHead({
	htmlAttrs: {
        lang: 'de'
    },
	link: [
		{rel: 'icon', type: 'image/x-icon', href: '/favicon.ico'}
	]
})
</script>

<style>
.link {
  @apply underline text-primary cursor-pointer;
}
</style>