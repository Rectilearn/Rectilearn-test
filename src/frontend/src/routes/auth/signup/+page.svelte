<script lang="ts">
	import { goto } from "$app/navigation";
	import { fetchApi, fetchUserData } from "$lib/api";
	import { Form } from "$lib/components/forms";

	let username = "";
	let email = "";
	let password = "";

	let errorMessages: string[] = [];

	async function handleSignup() {
		const response = await fetchApi("auth/users/create/", {
			method: "POST",
			body: JSON.stringify({
				email,
				name: username,
				password
			}),
			credentials: "omit"
		});

		if (response.ok) {
			fetchUserData().then(() => goto("/dashboard"));
		} else {
			errorMessages = [(await response.json())["detail"]];
		}
	}
</script>

<!-- bg -->
<div class="dark:bg-gray-900 h-full flex flex-col items-center justify-center flex-auto">
	<!-- container -->
	<div class="max-w-lg py-12 md:py-24 px-0 sm:px-8 w-full">
		<!-- vstack -->
		<div class="flex flex-col space-y-8">
			<!-- vstack -->
			<div class="flex flex-col space-y-6">
				<!-- vstack -->
				<div class="flex flex-col space-y-2 md:space-y-3 text-center">
					<h1 class="text-4xl font-bold">Sign up for an account</h1>
					<!-- hstack -->
					<div class="flex flex-row space-x-1 justify-center font-light">
						<p class="dark:text-gray-300">Already have an account?</p>
						<a href="/auth/login" class="text-[#90cdf4] hover:underline">Login</a>
					</div>
				</div>
			</div>
			<!-- Form -->
			<div
				class="py-6 sm:py-8 px-4 sm:px-10 bg-white dark:bg-[#2D3748] shadow-none sm:shadow-md rounded-xl"
			>
				<Form {errorMessages} on:submit={handleSignup}>
					<div class="flex flex-col space-y-6">
						<div class="flex flex-col space-y-5">
							<div class="flex flex-col space-y-2">
								<label for="email">Email</label>
								<input
									bind:value={email}
									id="email"
									type="email"
									name="email"
									class="dark:bg-black/[.16] border border-solid border-gray-300 dark:border-white/[.16] focus:outline-none hover:border-gray-500 hover:dark:border-white/[.24] focus:border-[#63b3ed] focus:shadow-[0_0_0_1px_#63b3ed] transition-[border-color] duration-200 px-3 py-2 rounded-md"
								/>
							</div>
							<div class="flex flex-col space-y-2">
								<label for="username">Username</label>
								<input
									id="username"
									bind:value={username}
									type="username"
									name="name"
									class="dark:bg-black/[.16] border border-solid border-gray-300 dark:border-white/[.16] focus:outline-none hover:border-gray-500 hover:dark:border-white/[.24] focus:border-[#63b3ed] focus:shadow-[0_0_0_1px_#63b3ed] transition-[border-color] duration-200 px-3 py-2 rounded-md"
								/>
							</div>
							<div class="flex flex-col space-y-2">
								<label for="password">Password</label>
								<input
									bind:value={password}
									id="password"
									type="password"
									name="password"
									class="dark:bg-black/[.16] border border-solid border-gray-300 dark:border-white/[.16] focus:outline-none hover:border-gray-500 hover:dark:border-white/[.24] focus:border-[#63b3ed] focus:shadow-[0_0_0_1px_#63b3ed] transition-[border-color] duration-200 px-3 py-2 rounded-md"
								/>
							</div>
						</div>
						<button
							type="submit"
							class="bg-[#4299e1] py-2 rounded-md text-white hover:scale-[1.01] duration-200"
							>Sign Up</button
						>
					</div>
				</Form>
			</div>
		</div>
	</div>
</div>

<style lang="scss">
	body {
		@apply bg-[rgb(247,_250,_252)];
		background-image: none;
	}
</style>
