<script>
	import { browser } from '$app/environment';
	import { page } from '$app/stores';
	import { PUBLIC_KIT_SITE_URL, PUBLIC_LEARN_SITE_URL } from '$env/static/public';
	import { Icon, Shell } from '@sveltejs/site-kit/components';
	import { Nav, Separator } from '@sveltejs/site-kit/nav';
	import { Search, SearchBox } from '@sveltejs/site-kit/search';
	import '@sveltejs/site-kit/styles/index.css';

	export let data;

	/** @type {import('@sveltejs/kit').Snapshot<number>} */
	let shell_snapshot;

	export const snapshot = {
		capture() {
			return {
				shell: shell_snapshot?.capture()
			};
		},
		restore(data) {
			shell_snapshot?.restore(data.shell);
		}
	};
</script>

<svelte:head>
	{#if !$page.route.id?.startsWith('/blog/')}
		<meta name="twitter:card" content="summary" />
		<meta name="twitter:image" content="https://svelte.dev/images/twitter-thumbnail.jpg" />
		<meta name="og:image" content="https://svelte.dev/images/twitter-thumbnail.jpg" />
	{/if}
</svelte:head>

<div style:display={$page.url.pathname !== '/docs' ? 'contents' : 'none'}>
	<Shell
		nav_visible={$page.url.pathname !== '/repl/embed'}
		bind:snapshot={shell_snapshot}
		banner_bottom_height="42px"
	>
		<Nav slot="top-nav" title={data.nav_title} links={data.nav_links}>
			<svelte:fragment slot="theme-label">Thème</svelte:fragment>
			<svelte:fragment slot="home-large">
				<strong>svelte</strong>.dev
			</svelte:fragment>

			<svelte:fragment slot="home-small">
				<strong>svelte</strong>
			</svelte:fragment>

			<svelte:fragment slot="search">
				{#if $page.url.pathname !== '/search'}
					<Search label="Recherche" />
				{/if}
			</svelte:fragment>

			<svelte:fragment slot="external-links">
				<a href={PUBLIC_LEARN_SITE_URL}>Tutoriel</a>

				<a href={PUBLIC_KIT_SITE_URL}>SvelteKit</a>

				<Separator />

				<a href="/chat" title="Discord Chat">
					<span class="small">Discord</span>
					<span class="large"><Icon name="discord" /></span>
				</a>

				<a href="https://github.com/sveltejs/svelte" title="GitHub Repo">
					<span class="small">GitHub</span>
					<span class="large"><Icon name="github" /></span>
				</a>
			</svelte:fragment>
		</Nav>

		<slot />
	</Shell>
</div>

{#if browser}
	<SearchBox placeholder="Recherche">
		<svelte:fragment slot="search-description">
			Les résultats se mettent à jour quand vous écrivez
		</svelte:fragment>
		<svelte:fragment slot="idle" let:has_recent_searches>
			{has_recent_searches ? 'Recherches récentes' : 'Aucune recherche récente'}
		</svelte:fragment>
		<svelte:fragment slot="no-results">Aucun résultat</svelte:fragment>
	</SearchBox>
{/if}

<style>
	:global(:root) {
		color-scheme: light dark;
	}

	:global(html, body) {
		height: 100%;
		width: 100%;
	}

	:global(.text .vo a) {
		color: var(--sk-text-1);
		box-shadow: inset 0 -1px 0 0 var(--sk-text-4);
		transition: color 0.2s ease-in-out;
	}

	:global(.text .vo a:hover) {
		color: var(--sk-text-3);
	}
</style>
