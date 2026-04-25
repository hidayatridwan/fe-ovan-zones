<script lang="ts">
	import { resolve } from '$app/paths';
	import type { Action } from 'svelte/action';

	type RevealOptions = {
		x?: number;
		y?: number;
		scale?: number;
		rotate?: number;
		blur?: number;
		delay?: number;
		duration?: number;
		threshold?: number;
		once?: boolean;
	};

	const navItems = [
		{ href: '/#events', label: 'Acara' },
		{ href: '/#history', label: 'Riwayat' },
		{ href: '/#services', label: 'Layanan' },
		{ href: '/#clients', label: 'Klien' },
		{ href: '/#contact', label: 'Kontak' }
	] as const;

	const eventCards = [
		{
			title: 'NEON VOID',
			date: '24 Okt',
			location: 'Berlin',
			tags: ['Techno', 'Habis'],
			image:
				'https://lh3.googleusercontent.com/aida-public/AB6AXuDIQswBT9gKHw8jT4atl1LPJ1jUaq7kijSKN4Dgw-9NmtOwxZCBh0Zj4GUy31i8YVdsbyw8hj4BfV0M5rX6kZb6NXW0pkg0-OD3TfxQfNY0ygcIvTLA_k6HeUiLc5meZ8-uDQZZlmbKpAIWHaKmbqo7ZFiWgQz2T3zO6T9r8KqZbuLNMdubmFj459ITJ-milmiwiR5sVAmGUYHCBhFBXs3cyup84yFtwdC4rg_RLiKE65XC0ODHh7d9Ohm69YYL8X_91f0_ihEtHvw',
			alt: 'Poster konser neon dengan siluet DJ dan gelombang audio oranye kebiruan'
		},
		{
			title: 'VELVET RHYTHM',
			date: '02 Nov',
			location: 'Paris',
			tags: ['Live Jazz'],
			image:
				'https://lh3.googleusercontent.com/aida-public/AB6AXuBRFewSRVAQ8g4c5V-cxo4YmDAxdokmYTn4LS7ykN7RjxLYweU_PGQUXNjIar3KWO-HTAyYbS5fa5m56JXKW-t7Q1Z7NnMd1iB64Ztr9pWAahYhR5jG7S6Z_V6FdxY2FM9qpHCN5uaYxae5kJBGnWeYHaMa11Lhs_uTlymPmfTfk2m4OvTl-Z-8-jgfWYQvFDfHNVi-LVNoAbNhWTxIdWb5dCMREMKVhfx-PxCsNXjUM4cyvNgqaEAbkdMCv1YWv6yx6iI_R5OHXEY',
			alt: 'Poster acara musik elegan di rooftop lounge malam hari'
		},
		{
			title: 'KINETIC PULSE',
			date: '15 Nov',
			location: 'London',
			tags: ['Electronic'],
			image:
				'https://lh3.googleusercontent.com/aida-public/AB6AXuBKG5IkfGL8pOwgrTZvDOGi6rAr7zW9OF1Zr7Kn9D7584BHPt_bb_OWJGR2XOK7abSEBWzsoqxdwyxoVnRELSdO-O0N34lL5Twz5iZoGxAJzUbvCE-tf25uGV1XejrWhyGH_KI91o4ph-gz8ArBTzIiqQojfTHtL6kp7qfYdWolTRsZ6m0bI2IJfskvyep-3aw_PxmmNlwOvLBg2-EmHj3BJrxIaK82q3zFtBM1uqJVu1_0zlZ3rZd2Bx-uS7MLGdJ2xrmyY5PUKPI',
			alt: 'Suasana rave bawah tanah dengan strobe oranye dan gerakan penonton'
		},
		{
			title: 'ECHO FEST',
			date: '05 Des',
			location: 'New York',
			tags: ['Alternative'],
			image:
				'https://lh3.googleusercontent.com/aida-public/AB6AXuDwFmG6LndnBD3doyMJL60r0AiN5e1_0mhjQyKJ1rsazqnmm8K3JpubZSGKRmxp9MTDEUBwm_hb9-voB7TH9N3kepZtHnaTIL5v-XKkl8ZZMboo1oEJrZf5gFkKq4Tc7K5gTIaPlvbqokbfyhK8vVmPI5264cr2nqwpTco0PTXqby341Eixurg7okPDTFYHf9j8zmpJ1ATBqxvYg9q6UqTz9bjnwrrUuCwkWwMNmf9-84sXhOwmGuw4QyDQuAvGUuonCOZyibM1QVA',
			alt: 'Festival luar ruang saat matahari terbenam dengan panggung besar dan kerumunan'
		}
	];

	const historyItems = [
		{
			season: 'Musim Panas 2023',
			title: 'Panggung The Oracle',
			description:
				'Festival imersif tiga hari yang mendefinisikan ulang produksi audio-visual dengan sistem suara 360 derajat.',
			image:
				'https://lh3.googleusercontent.com/aida-public/AB6AXuAXYu41PLYk7WbDbaxhZdF6lGGQz66jS_inrt-mCrHbtv_C-Kji9dx9f51Ae2kZ8MNI4tufom5m_MQIKRc56iUVsA1ut-XDK6u2FbjT5sY7gJOLqNlj4eDXmGKLIvkvfqj9FiAUdD5U9tQoazexMz_64H7C9zGdyEGz8SAtqweSdRbqKg2i8B_uZoxzCRTaBCctTJCxgUu6Uq4J3KRmOdWKwGFDr2m8lny6zHPTwQGqmIR6pb8XtyfOBMPl0jF7kXmNCvv01URwbjk',
			alt: 'Fotografi panggung festival besar dengan desain cahaya geometris'
		},
		{
			season: 'Musim Dingin 2022',
			title: 'Sesi Subterranean',
			description:
				'Acara gudang bawah tanah eksklusif yang menampilkan pionir techno eksperimental dan tata lampu industrial.',
			image:
				'https://lh3.googleusercontent.com/aida-public/AB6AXuBPP9xLlD_0w0UThJWFpPASHLUf7pRPorD7gdNx5wlk4OpLVafO7O5lTFyf-0AAB-MSSm-bYlOt-QZpHciuAjjIa09crSKYraSaz5q6_58o_23o0jIA2uApcstVFXpLdCDB0KyZ1xSJulXPy0Q1XGGBycUY0GPcMh7c4GKS8ZwxilPOb0PSLvGVeJHenqH7G04wLdID1__En1l9PhbmDVcIpzwgTb3411gmjDgc9SWUxjw-EfrwBED53Hm8DMHhBGIU8BuNrgRk8sw',
			alt: 'Interior gudang industrial dengan booth DJ oranye menyala'
		}
	];

	const services = [
		{
			icon: 'piano',
			title: 'Penyewaan Alat',
			description:
				'Solusi backline kelas tur untuk produksi profesional, dari synth vintage sampai grand piano premium.'
		},
		{
			icon: 'celebration',
			title: 'Acara Pernikahan',
			description:
				'Kurasi musik privat untuk pernikahan mewah dengan detail panggung, mood, dan transisi acara yang presisi.'
		},
		{
			icon: 'groups',
			title: 'Komunitas',
			description:
				'Dukungan untuk artis lokal melalui workshop, malam open-mic, showcase kolektif, dan festival jejaring.'
		},
		{
			icon: 'stadium',
			title: 'Konser Besar',
			description:
				'Manajemen produksi menyeluruh untuk konser skala stadion, tur, dan event brand dengan kebutuhan kompleks.'
		}
	];

	const clients = ['SONY MUSIC', 'UNIVERSAL', 'LOCAL FEST', 'WARNER', 'INDIE GIGS', 'EVENT X'];

	const stats = [
		{ value: '220+', label: 'Acara Terkurasi' },
		{ value: '48', label: 'Kota Aktif' },
		{ value: '1.8M', label: 'Penonton' }
	];

	const revealPresets: RevealOptions[] = [
		{ y: 52, blur: 10, duration: 760 },
		{ x: -48, y: 18, blur: 6, duration: 720 },
		{ x: 48, y: 18, scale: 0.96, duration: 760 },
		{ y: 24, scale: 0.9, rotate: -1.5, blur: 8, duration: 820 },
		{ y: -22, scale: 0.98, duration: 700 }
	];

	const cardMotion = (index: number): RevealOptions => ({
		...revealPresets[index % revealPresets.length],
		delay: 110 + index * 90
	});

	const reveal: Action<HTMLElement, RevealOptions | undefined> = (node, options = {}) => {
		const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

		if (prefersReducedMotion) {
			return {};
		}

		const config = {
			x: 0,
			y: 44,
			scale: 1,
			rotate: 0,
			blur: 0,
			delay: 0,
			duration: 720,
			threshold: 0.18,
			once: true,
			...options
		};

		const fromTransform = `translate3d(${config.x}px, ${config.y}px, 0) scale(${config.scale}) rotate(${config.rotate}deg)`;
		const toTransform = 'translate3d(0, 0, 0) scale(1) rotate(0deg)';
		const easing = 'cubic-bezier(0.22, 1, 0.36, 1)';

		node.style.opacity = '0';
		node.style.transform = fromTransform;
		node.style.filter = config.blur ? `blur(${config.blur}px)` : 'none';
		node.style.transition = [
			`opacity ${config.duration}ms ${easing}`,
			`transform ${config.duration}ms ${easing}`,
			`filter ${config.duration}ms ${easing}`
		].join(', ');
		node.style.transitionDelay = `${config.delay}ms`;
		node.style.willChange = 'opacity, transform, filter';

		const show = () => {
			node.style.opacity = '1';
			node.style.transform = toTransform;
			node.style.filter = 'blur(0)';
		};

		const hide = () => {
			node.style.opacity = '0';
			node.style.transform = fromTransform;
			node.style.filter = config.blur ? `blur(${config.blur}px)` : 'none';
		};

		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) {
					show();

					if (config.once) {
						observer.disconnect();
					}

					return;
				}

				if (!config.once) {
					hide();
				}
			},
			{
				threshold: config.threshold,
				rootMargin: '0px 0px -10% 0px'
			}
		);

		observer.observe(node);

		return {
			destroy() {
				observer.disconnect();
			}
		};
	};
</script>

<svelte:head>
	<title>OvanZone | Pengalaman Musik Terbaik</title>
	<meta
		name="description"
		content="OvanZone menghadirkan konser, festival, penyewaan alat, dan produksi event musik dengan pengalaman panggung imersif."
	/>
</svelte:head>

<header
	class="fixed top-0 z-50 w-full border-b border-white/10 bg-zinc-950/80 shadow-[0_4px_30px_rgba(0,0,0,0.5)] backdrop-blur-lg"
	use:reveal={{ y: -20, duration: 520 }}
>
	<nav class="mx-auto flex h-20 max-w-[1280px] items-center justify-between gap-5 px-5 sm:px-6">
		<a
			class="font-h1 text-2xl font-black text-orange-600"
			href={resolve('/')}
			aria-label="OvanZone home"
		>
			OvanZone
		</a>

		<div class="font-button hidden items-center gap-8 text-sm md:flex">
			{#each navItems as item (item.href)}
				<a
					class="text-zinc-400 transition-colors duration-300 hover:text-orange-500"
					href={resolve(item.href)}
				>
					{item.label}
				</a>
			{/each}
		</div>

		<a
			class="bg-primary-container font-button text-button text-on-primary-container inline-flex min-h-11 items-center justify-center px-4 py-3 font-semibold uppercase transition-all duration-300 hover:shadow-[0_0_20px_rgba(255,106,0,0.5)] active:scale-95 sm:px-6"
			href="#events"
		>
			Beli Tiket
		</a>
	</nav>
</header>

<main class="text-on-surface min-h-screen overflow-hidden bg-[#0B0B0B]">
	<section
		class="relative flex min-h-[90svh] items-center justify-center overflow-hidden pt-28 pb-20"
	>
		<div class="absolute inset-0 z-0">
			<img
				class="hero-ken-burns h-full w-full object-cover opacity-60"
				alt="Panggung festival musik malam hari dengan sorotan lampu oranye dan ungu serta siluet penonton"
				src="https://lh3.googleusercontent.com/aida-public/AB6AXuDeg4gKniH7iWdIAIyo5R8pMOV9AoG57fFn17fiybKNoWYY5tDXol7X6qAFNx6kcNsbkrY5KZ_YDxuZK31t4YJrHepPffzoTCb0qBBCLlX7kWzXWtUIZdlu4b2Es0GPpwx2d0GSxWIx6sIJOynqJ_evAS5PqzyUvEuZHiffQu9BxtRtcqapovGsIas1WDZmYR1uoPgPz-Ybaay9o4jlxYq8_Ali2fEIJhGkrN0OHzQPKH6MdUgXLTdaaq3hUFs-ps1JTATOpE7ZZTY"
			/>
			<div
				class="absolute inset-0 bg-gradient-to-b from-black/15 via-[#0B0B0B]/45 to-[#0B0B0B]"
			></div>
			<div
				class="absolute inset-x-0 bottom-0 h-32 bg-gradient-to-t from-[#0B0B0B] to-transparent"
			></div>
		</div>

		<div class="relative z-10 mx-auto max-w-[1280px] px-5 text-center sm:px-6">
			<div use:reveal={{ y: 58, blur: 12, duration: 850 }}>
				<p class="font-button text-primary-container mb-5 text-sm font-semibold uppercase">
					Konser, festival, dan produksi live
				</p>
				<h1
					class="font-h1 lg:text-h1 mx-auto mb-6 max-w-5xl text-5xl leading-[1.08] font-black text-white uppercase sm:text-6xl"
				>
					OVANZONE LIVE EXPERIENCE
				</h1>
				<p class="font-body-lg text-body-lg mx-auto mb-10 max-w-2xl leading-relaxed text-zinc-300">
					Melampaui batas hiburan langsung. Temukan perjalanan sonik yang dikurasi, visual panggung
					imersif, dan atmosfer kehidupan malam yang eksklusif.
				</p>
			</div>

			<div
				class="mb-12 flex flex-col justify-center gap-4 sm:flex-row"
				use:reveal={{ y: 34, scale: 0.96, delay: 180, duration: 700 }}
			>
				<a
					class="bg-primary-container font-button text-button text-on-primary-container inline-flex min-h-14 items-center justify-center px-8 py-5 font-semibold uppercase transition-all duration-300 hover:shadow-[0_0_30px_rgba(255,106,0,0.6)] active:scale-95 sm:px-10"
					href="#events"
				>
					Jelajahi Acara
				</a>
				<a
					class="font-button text-button hover:border-primary-container/60 inline-flex min-h-14 items-center justify-center border border-white/20 px-8 py-5 font-semibold text-white uppercase transition-all duration-300 hover:bg-white/5 active:scale-95 sm:px-10"
					href="#history"
				>
					Tonton Cuplikan
				</a>
			</div>

			<div
				class="mx-auto grid max-w-3xl grid-cols-1 border border-white/10 bg-black/35 backdrop-blur-md sm:grid-cols-3"
				use:reveal={{ y: 26, blur: 8, delay: 280, duration: 760 }}
			>
				{#each stats as stat (stat.label)}
					<div class="border-white/10 px-6 py-5 text-left sm:border-l sm:first:border-l-0">
						<p class="font-h3 text-3xl font-bold text-white">{stat.value}</p>
						<p class="font-body-md mt-1 text-sm text-zinc-400">{stat.label}</p>
					</div>
				{/each}
			</div>
		</div>
	</section>

	<section class="py-xl relative overflow-hidden" id="events" use:reveal={revealPresets[0]}>
		<div class="stage-glow absolute inset-0 -z-10"></div>
		<div class="mx-auto max-w-[1280px] px-5 sm:px-6">
			<div class="mb-12 flex flex-col gap-6 sm:flex-row sm:items-end sm:justify-between">
				<div>
					<p class="font-button text-primary-container mb-3 text-sm font-semibold uppercase">
						Lineup terkurasi
					</p>
					<h2 class="font-h2 md:text-h2 text-4xl font-bold text-white uppercase">
						Acara Mendatang
					</h2>
					<div class="bg-primary-container mt-4 h-1 w-24"></div>
				</div>
				<a
					class="font-button text-button text-primary-container font-semibold uppercase hover:underline"
					href="#events"
				>
					Lihat Semua
				</a>
			</div>

			<div class="gap-gutter grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4">
				{#each eventCards as event, index (event.title)}
					<article
						class="neon-glow-hover group relative overflow-hidden bg-[#1F1F1F] transition-all duration-500"
						use:reveal={cardMotion(index)}
					>
						<div class="aspect-[3/4] overflow-hidden">
							<img
								class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
								alt={event.alt}
								src={event.image}
								loading="lazy"
							/>
						</div>
						<div
							class="absolute inset-0 bg-gradient-to-t from-[#0B0B0B] via-transparent to-transparent opacity-90"
						></div>
						<div class="absolute bottom-0 w-full p-6">
							<div class="mb-3 flex flex-wrap gap-2">
								{#each event.tags as tag, tagIndex (tag)}
									<span
										class={tagIndex === 0
											? 'bg-primary-container text-on-primary-container px-2 py-1 text-[10px] font-bold uppercase'
											: 'bg-zinc-800 px-2 py-1 text-[10px] font-bold text-white uppercase'}
									>
										{tag}
									</span>
								{/each}
							</div>
							<h3 class="font-h3 mb-1 text-xl font-bold text-white">{event.title}</h3>
							<p class="font-label-sm flex items-center gap-1 text-sm text-zinc-400 uppercase">
								<span class="material-symbols-outlined text-sm" aria-hidden="true">
									calendar_today
								</span>
								{event.date} - {event.location}
							</p>
						</div>
					</article>
				{/each}
			</div>
		</div>
	</section>

	<section class="py-xl bg-[#0B0B0B]" id="history" use:reveal={revealPresets[1]}>
		<div class="mx-auto max-w-[1280px] px-5 sm:px-6">
			<div
				class="mb-16 flex flex-col gap-6 sm:flex-row sm:items-end sm:justify-between"
				use:reveal={{ y: 36, blur: 8, duration: 720 }}
			>
				<div>
					<p class="font-button text-primary-container mb-3 text-sm font-semibold uppercase">
						Rekam jejak
					</p>
					<h2 class="font-h2 md:text-h2 text-4xl font-bold text-white uppercase">
						Momen Legendaris
					</h2>
				</div>
				<a
					class="font-button text-button text-primary-container font-semibold uppercase hover:underline"
					href="#history"
				>
					Lihat Semua
				</a>
			</div>

			<div class="relative">
				<div
					class="absolute left-1/2 hidden h-full w-px -translate-x-1/2 bg-white/10 md:block"
				></div>
				<div class="space-y-md">
					{#each historyItems as item, index (item.title)}
						<article
							class={index % 2 === 1
								? 'flex flex-col items-center gap-10 md:flex-row-reverse'
								: 'flex flex-col items-center gap-10 md:flex-row'}
							use:reveal={cardMotion(index + 2)}
						>
							<div class="w-full md:w-1/2">
								<div
									class={index % 2 === 0
										? 'glass-card border-primary-container w-full border-l-4 p-6 sm:p-8'
										: 'glass-card border-primary-container w-full border-r-4 p-6 sm:p-8'}
								>
									<p class="font-body-md text-primary-container mb-2 text-sm font-bold uppercase">
										{item.season}
									</p>
									<h3 class="font-h3 mb-2 text-xl font-bold text-white uppercase">
										{item.title}
									</h3>
									<p class="text-sm leading-relaxed text-zinc-400">{item.description}</p>
								</div>
							</div>
							<div class="md:w-1/2">
								<img
									class="h-56 w-full object-cover grayscale transition-all duration-500 hover:grayscale-0"
									alt={item.alt}
									src={item.image}
									loading="lazy"
								/>
							</div>
						</article>
					{/each}
				</div>
			</div>
		</div>
	</section>

	<section class="py-xl relative bg-[#0B0B0B]" id="services" use:reveal={revealPresets[2]}>
		<div class="mx-auto max-w-[1280px] px-5 sm:px-6">
			<div class="mb-12 max-w-2xl" use:reveal={{ x: -36, blur: 8, duration: 720 }}>
				<p class="font-button text-primary-container mb-3 text-sm font-semibold uppercase">
					Produksi end-to-end
				</p>
				<h2 class="font-h2 md:text-h2 text-4xl font-bold text-white uppercase">Layanan Kami</h2>
			</div>

			<div class="gap-gutter grid grid-cols-1 md:grid-cols-2">
				{#each services as service, index (service.title)}
					<article
						class="glass-card group hover:border-primary-container/30 flex gap-6 p-6 transition-colors sm:p-8"
						use:reveal={cardMotion(index + 4)}
					>
						<div
							class="bg-primary-container/10 text-primary-container flex size-16 shrink-0 items-center justify-center"
						>
							<span class="material-symbols-outlined text-4xl" aria-hidden="true">
								{service.icon}
							</span>
						</div>
						<div>
							<h3 class="font-h3 mb-3 text-2xl font-bold text-white">{service.title}</h3>
							<p class="leading-relaxed text-zinc-400">{service.description}</p>
						</div>
					</article>
				{/each}
			</div>
		</div>
	</section>

	<section class="py-xl bg-[#0B0B0B]" id="clients" use:reveal={revealPresets[3]}>
		<div class="mx-auto max-w-[1280px] px-5 sm:px-6">
			<div class="mb-12 max-w-3xl">
				<p class="font-button text-primary-container mb-3 text-sm font-semibold uppercase">
					Kolaborasi
				</p>
				<h2 class="font-h2 md:text-h2 text-4xl font-bold text-white uppercase">Klien Kami</h2>
				<p class="font-body-md mt-4 max-w-2xl text-sm leading-relaxed text-zinc-400">
					Dipercaya oleh label, promotor, kolektif kreatif, dan brand experience untuk menghadirkan
					produksi yang tajam.
				</p>
			</div>

			<div class="grid grid-cols-2 items-center gap-4 opacity-70 md:grid-cols-3 lg:grid-cols-6">
				{#each clients as client, index (client)}
					<div
						class="flex justify-center p-3 transition-all duration-300 hover:opacity-100 hover:grayscale-0"
						use:reveal={cardMotion(index)}
					>
						<div
							class="hover:border-primary-container/60 w-full border-2 border-white/20 px-3 py-4 text-center text-sm font-bold text-white transition-colors duration-300"
						>
							{client}
						</div>
					</div>
				{/each}
			</div>
		</div>
	</section>

	<section class="py-xl bg-[#0B0B0B]" id="contact" use:reveal={revealPresets[4]}>
		<div class="mx-auto max-w-[1280px] px-5 sm:px-6">
			<div class="gap-margin flex flex-col lg:flex-row">
				<div class="lg:w-1/2" use:reveal={{ x: -42, blur: 8, duration: 760 }}>
					<p class="font-button text-primary-container mb-3 text-sm font-semibold uppercase">
						Mulai produksi
					</p>
					<h2 class="font-h2 md:text-h2 mb-8 text-4xl font-bold text-white uppercase">
						Hubungi Kami
					</h2>
					<form class="space-y-6" aria-label="Form kontak OvanZone">
						<div class="grid grid-cols-1 gap-6 md:grid-cols-2">
							<label class="block">
								<span class="font-label-sm mb-2 block text-sm text-zinc-500 uppercase">Nama</span>
								<input
									class="focus:border-primary-container w-full border border-white/10 bg-[#1F1F1F] px-4 py-4 text-white transition-colors focus:outline-none"
									type="text"
									name="name"
									autocomplete="name"
								/>
							</label>
							<label class="block">
								<span class="font-label-sm mb-2 block text-sm text-zinc-500 uppercase">Email</span>
								<input
									class="focus:border-primary-container w-full border border-white/10 bg-[#1F1F1F] px-4 py-4 text-white transition-colors focus:outline-none"
									type="email"
									name="email"
									autocomplete="email"
								/>
							</label>
						</div>
						<label class="block">
							<span class="font-label-sm mb-2 block text-sm text-zinc-500 uppercase">
								Tipe Proyek
							</span>
							<select
								class="focus:border-primary-container w-full border border-white/10 bg-[#1F1F1F] px-4 py-4 text-white transition-colors focus:outline-none"
								name="project_type"
							>
								<option>Produksi Konser</option>
								<option>Pemesanan Privat</option>
								<option>Inkuiri Penyewaan</option>
							</select>
						</label>
						<label class="block">
							<span class="font-label-sm mb-2 block text-sm text-zinc-500 uppercase">Pesan</span>
							<textarea
								class="focus:border-primary-container min-h-36 w-full border border-white/10 bg-[#1F1F1F] px-4 py-4 text-white transition-colors focus:outline-none"
								name="message"
							></textarea>
						</label>
						<button
							class="bg-primary-container font-button text-button text-on-primary-container w-full py-5 font-semibold uppercase transition-all hover:shadow-[0_0_20px_rgba(255,106,0,0.4)] active:scale-[0.99]"
							type="submit"
						>
							Kirim Pesan
						</button>
					</form>
				</div>

				<div class="flex flex-col gap-6 lg:w-1/2" use:reveal={{ x: 42, blur: 8, duration: 760 }}>
					<div class="glass-card flex flex-grow flex-col gap-10 p-6 md:flex-row md:p-8">
						<div class="space-y-6">
							<h3 class="font-h3 text-xl font-bold text-white uppercase">Detail Kontak</h3>
							<div class="space-y-4">
								<a class="group flex items-center gap-4" href="mailto:hello@ovanzone.events">
									<span class="material-symbols-outlined text-primary-container" aria-hidden="true">
										mail
									</span>
									<span class="text-zinc-300 transition-colors group-hover:text-white">
										hello@ovanzone.events
									</span>
								</a>
								<a class="group flex items-center gap-4" href="tel:+622179460123">
									<span class="material-symbols-outlined text-primary-container" aria-hidden="true">
										call
									</span>
									<span class="text-zinc-300 transition-colors group-hover:text-white">
										+62 21 7946 0123
									</span>
								</a>
								<div class="flex items-center gap-4">
									<span class="material-symbols-outlined text-primary-container" aria-hidden="true">
										distance
									</span>
									<span class="text-zinc-300">Creative Quarter, Jakarta ID</span>
								</div>
							</div>
						</div>

						<div class="map-panel relative min-h-[300px] flex-grow overflow-hidden">
							<div class="absolute inset-0 opacity-60"></div>
							<div class="absolute inset-0 flex items-center justify-center">
								<div
									class="bg-primary-container/20 absolute size-16 animate-ping rounded-[999px]"
								></div>
								<div
									class="bg-primary-container absolute size-5 rounded-[999px] shadow-[0_0_15px_#FF6A00]"
								></div>
								<div
									class="absolute mt-24 bg-black/70 px-3 py-2 text-xs font-semibold text-white uppercase"
								>
									Jakarta HQ
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
</main>

<footer class="border-t border-zinc-800 bg-zinc-950">
	<div
		class="mx-auto flex max-w-[1280px] flex-col items-center justify-between gap-6 px-5 py-12 md:flex-row md:px-8"
	>
		<a class="font-h1 text-xl font-black text-orange-600" href={resolve('/')}>OvanZone</a>
		<div class="font-button flex flex-wrap justify-center gap-6 text-sm uppercase md:gap-8">
			<a class="text-zinc-500 transition-all hover:text-white" href="https://www.instagram.com/">
				Instagram
			</a>
			<a class="text-zinc-500 transition-all hover:text-white" href="https://open.spotify.com/">
				Spotify
			</a>
			<a class="text-zinc-500 transition-all hover:text-white" href="#contact">Privasi</a>
			<a class="text-zinc-500 transition-all hover:text-white" href="#contact">Ketentuan</a>
		</div>
		<p class="font-button text-center text-sm text-zinc-500 uppercase md:text-right">
			© 2026 OvanZone Events. Hak cipta dilindungi.
		</p>
	</div>
</footer>
