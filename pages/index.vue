<script setup lang="ts">
import QrcodeVue from 'qrcode.vue'

definePageMeta({
	layout: 'default'
})

let blockedDomains = ref(0)

async function getBlockedDomains() {
	const res = await fetch(useRuntimeConfig().public.api_root + '/blocked_domains')
	const data = await res.json()
	blockedDomains.value = data.length
}

onMounted(() => {
	getBlockedDomains()
})
</script>

<template>
	<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
		<div class="bg-base-300 shadow-lg p-4">
			<div class="bg-cuii-banner-background bg-cover bg-center h-64 mb-1">
				<div class="flex flex-col items-center justify-center h-full text-center p-2">
					<div class="text-white text-2xl font-bold">Diese Webseite ist aus urheberrechtlichen Gründen nicht
						verfügbar.
					</div>
					<div class="text-white">Die CUII veranlasst die Sperrung dieser Seite – oft ohne tiefgehende
						richterliche
						Prüfung.
					</div>
				</div>
			</div>
			<h2 class="text-2xl font-bold">
				Fragwürdige Gerichtsbeschlüsse
			</h2>
			<p>
				Die CUII ist ein privater Zusammenschluss, der Internetsperren durchsetzt. Zwar stützt man sich
				mittlerweile auf Gerichtsurteile, oft handelt es sich dabei jedoch um sogenannte Versäumnisurteile:
				Erscheint ein Internetanbieter nicht vor Gericht, wird die Sperre ohne tiefe inhaltliche Prüfung
				erlassen - und alle anderen Provider ziehen "freiwillig" mit.
			</p>
		</div>

		<div class="bg-base-300 shadow-lg p-4 flex flex-col justify-between">
			<div>
				<h2 class="text-2xl font-bold">
					"Transparente" Sperrliste
				</h2>
				<p class="mt-2">
					Die CUII sperrt Domains. Welche genau? Das wird von der CUII nicht preisgegeben.
				</p>
				<p>
					Aber keine Sorge - <b>dafür gibt es ja uns</b>.
					Wir geben unser Bestes, um alle gesperrten Domains zu sammeln und zu veröffentlichen.
				</p>
			</div>
			<div class="mx-2 bottom-0 align-bottom">
				<NuxtImg src="/img/nicht_genannt.webp" class="w-full"/>
				<p class="text-[--lessimportant] italic">
					Zitat aus Anlage 1 §4 Abs. 4 lit. l des
					<a class="link" href="https://cuii.info/fileadmin/files/CUII_Verhaltenskodex_23.pdf"
					   target="_blank">CUII-Verhaltenskodex</a>
					<br class="hidden sm:block"/>
					SUW = Strukturell urheberrechtsverletzende Webseite
				</p>
			</div>
		</div>
		<div class="bg-base-300 shadow-lg p-4 flex flex-col">
			<h2 class="text-2xl font-bold">
				Unsere Ziele
			</h2>
			<ul class="list-disc ml-6 mt-2">
				<li>
					<b>Transparenz:</b> Wir wollen die Sperrpraxis der CUII transparent machen.
				</li>
				<li>
					<b>Meinungsfreiheit:</b> Wir wollen die Meinungsfreiheit im Internet schützen.
				</li>
				<li>
					<b>Freies Internet:</b> Wir sind für eine Welt, in der das Internet frei und offen ist.
				</li>
				<li>
					<b>Keine Zensur:</b> Wir sind gegen Zensur durch private Organisationen.
				</li>
			</ul>
		</div>
		<div class="flex flex-col justify-between">
			<NuxtLink class="bg-primary shadow-lg p-4 flex hover:bg-primary-hover mb-2 hover:shadow-xl" to="/umgehen">
				<Icon name="eos-icons:dns" class="text-white text-6xl"/>
				<div class="flex flex-col ml-4">
					<h2 class="text-white text-2xl font-bold">
						Zensur umgehen
					</h2>
					<p class="text-white">
						Wir zeigen Ihnen wie Sie <b>ganz einfach</b> die intransparenten Netzsperren der CUII umgehen
						können.
					</p>
				</div>
				<Icon name="mdi:arrow-right" class="text-white text-6xl ml-auto"/>
			</NuxtLink>
			<NuxtLink class="bg-accent shadow-lg p-4 flex hover:bg-primary-hover mt-2 hover:shadow-xl" to="/domains">
				<Icon name="octicon:blocked-16" class="text-white text-6xl"/>
				<div class="flex flex-col ml-4">
					<h2 class="text-white text-2xl font-bold">
						Gesperrte Domains
					</h2>
					<p class="text-white">
						Die CUII hat im Moment <b>{{ blockedDomains }}</b> Domains gesperrt. Schau dir die Liste an!
					</p>
				</div>
				<Icon name="mdi:arrow-right" class="text-white text-6xl ml-auto"/>
			</NuxtLink>
		</div>
		<div class="bg-base-300 shadow-lg p-4 flex flex-col">
			<div>
				<h2 class="text-2xl font-bold mb-2">
					Socials
				</h2>
				<p class="text-white/80">
					Tritt unserem Discord-Server oder Matrix-Space bei um Benachrichtigungen zu erhalten oder
					Informationen auszutauschen.
				</p>
			</div>

			<div class="grid grid-cols-[1fr_auto_1fr] gap-3 items-center">

				<a class="bg-primary text-white py-3 px-4 rounded-lg flex items-center justify-center gap-2 hover:bg-primary-hover w-full transition-colors"
				   :href="useRuntimeConfig().public.discord_invite">
					<span>Beitreten</span>
					<Icon name="pajamas:discord" class="text-xl"/>
				</a>

				<div class="flex items-center w-12 sm:w-16">
					<div class="h-[2px] flex-1 bg-white/20 rounded-full"></div>

					<div class="px-1">
						<Icon name="material-symbols:link" class="text-white/50 text-xl block"/>
					</div>

					<div class="h-[2px] flex-1 bg-white/20 rounded-full"></div>
				</div>

				<a class="bg-[#0dbd8b] text-white py-3 px-4 rounded-lg flex items-center justify-center gap-2 hover:brightness-110 w-full transition-colors"
				   :href="'https://matrix.to/#/'+useRuntimeConfig().public.matrix_space">
					<span class="truncate">{{ useRuntimeConfig().public.matrix_space }}</span>
					<Icon name="simple-icons:matrix" class="text-xl flex-shrink-0"/>
				</a>

			</div>
		</div>
		<div class="bg-base-300 shadow-lg p-4 flex flex-col">
			<div class="flex flex-col">
				<h2 class="text-2xl font-bold">
					Über uns
				</h2>
				<p>
					Erfahre mehr über uns, unsere Ziele und wie diese Webseite funzt.
				</p>
				<NuxtLink
					class="bg-base-100 p-3 px-5 m-auto rounded-lg flex items-center gap-2 hover:bg-primary-hover mt-2"
					to="/about">
					<span class="mr-2">Mehr erfahren</span>
					<Icon name="mdi:arrow-right" class="text-2xl"/>
				</NuxtLink>
			</div>
		</div>
	</div>
</template>

<style scoped>

</style>