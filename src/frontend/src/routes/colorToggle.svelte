<script lang="ts">
	import { browser } from '$app/environment';
	import { fly } from 'svelte/transition';

	let darkMode = true;

	function handleSwitchDarkMode() {
		darkMode = !darkMode;

		darkMode
			? document.documentElement.classList.add('dark')
			: document.documentElement.classList.remove('dark');
	}

	if (browser) {
		if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
			document.documentElement.classList.add('dark');
			darkMode = true;
		} else {
			document.documentElement.classList.remove('dark');
			darkMode = false;
		}
	}
</script>

<button on:click={handleSwitchDarkMode} id="themeToggle">
	<div class="h-6 w-5">
		{#if darkMode}
			<svg
				xmlns="http://www.w3.org/2000/svg"
				transition:fly={{ y: -30, duration: 300 }}
				viewBox="0 0 384 512"
				><!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path
					d="M223.5 32C100 32 0 132.3 0 256S100 480 223.5 480c60.6 0 115.5-24.2 155.8-63.4c5-4.9 6.3-12.5 3.1-18.7s-10.1-9.7-17-8.5c-9.8 1.7-19.8 2.6-30.1 2.6c-96.9 0-175.5-78.8-175.5-176c0-65.8 36-123.1 89.3-153.3c6.1-3.5 9.2-10.5 7.7-17.3s-7.3-11.9-14.3-12.5c-6.3-.5-12.6-.8-19-.8z"
				/></svg
			>
		{:else}
			<svg
				class="ml-[-2px]"
				xmlns="http://www.w3.org/2000/svg"
				transition:fly={{ y: 30, duration: 300 }}
				viewBox="0 0 512 512"
				><!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path
					d="M361.5 1.2c5 2.1 8.6 6.6 9.6 11.9L391 121l107.9 19.8c5.3 1 9.8 4.6 11.9 9.6s1.5 10.7-1.6 15.2L446.9 256l62.3 90.3c3.1 4.5 3.7 10.2 1.6 15.2s-6.6 8.6-11.9 9.6L391 391 371.1 498.9c-1 5.3-4.6 9.8-9.6 11.9s-10.7 1.5-15.2-1.6L256 446.9l-90.3 62.3c-4.5 3.1-10.2 3.7-15.2 1.6s-8.6-6.6-9.6-11.9L121 391 13.1 371.1c-5.3-1-9.8-4.6-11.9-9.6s-1.5-10.7 1.6-15.2L65.1 256 2.8 165.7c-3.1-4.5-3.7-10.2-1.6-15.2s6.6-8.6 11.9-9.6L121 121 140.9 13.1c1-5.3 4.6-9.8 9.6-11.9s10.7-1.5 15.2 1.6L256 65.1 346.3 2.8c4.5-3.1 10.2-3.7 15.2-1.6zM160 256a96 96 0 1 1 192 0 96 96 0 1 1 -192 0zm224 0a128 128 0 1 0 -256 0 128 128 0 1 0 256 0z"
				/></svg
			>
		{/if}
	</div>
</button>

<style lang="scss">
	#themeToggle {
		@apply w-auto appearance-none px-3 py-2 rounded-md font-bold
             text-gray-600 dark:text-inherit relative;

		&:hover {
			@apply no-underline bg-[#bee3f8] dark:bg-[#2D3748];
		}
		
		&:active {
			@apply bg-[#E2E8F0] dark:bg-[rgba(255,255,255,0.16)];
		}

		&:focus {
			@apply shadow-[0_0_0_3px_rgba(66,153,225,0.6)];
			// dark:shadow-[0_0_0_3px_rgba(66,153,225,0.6)];
		}
	}

	#themeToggle > div > svg {
		@apply h-6  fill-current absolute;
	}
	/* #theme-toggle {
        @apply invisible;
    }

    #theme-toggle + label {
        @apply inline-block cursor-pointer h-12 w-12 absolute top-6 right-24 rounded-full duration-300 content-[''];
    }

    #theme-toggle:not(:checked) + label {
        @apply bg-amber-400;
    }

    #theme-toggle:checked + label {
        @apply bg-transparent;
        box-shadow: inset -18px -16px 1px 1px #ddd;
    } */
</style>
