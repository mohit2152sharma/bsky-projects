<script lang="ts">
	import { Button } from '$lib/components/ui/button/index';
	import * as Card from '$lib/components/ui/card/index';
	import { Input } from '$lib/components/ui/input/index';
	import { Label } from '$lib/components/ui/label/index';
	import { superForm } from 'sveltekit-superforms';
	import type { PageData } from '../../routes/$types';
	import LoaderCircle from 'lucide-svelte/icons/loader-circle';
	import type { LoginCredentialsSchemaType } from '$lib/server/bsky/types';
	import LoadingButton from './custom-comps/loading-button.svelte';

	export let data: PageData & { form: LoginCredentialsSchemaType };
	const { form, submitting, enhance } = superForm(data.form);
</script>

<Card.Root class="mx-auto max-w-sm">
	<Card.Header>
		<Card.Title class="text-2xl">Login</Card.Title>
		<Card.Description>With your Bluesky Handle and App password</Card.Description>
	</Card.Header>
	<Card.Content>
		<form method="POST" use:enhance>
			<div class="grid gap-4">
				<div class="grid gap-2">
					<Label for="identifier">Bluesky Handle</Label>
					<Input
						id="identifier"
						name="identifier"
						placeholder="user.bsky.social"
						bind:value={$form.identifier}
						required
					/>
				</div>
				<div class="grid gap-2">
					<div class="flex items-center">
						<Label for="password">App Password</Label>
						<a
							href="https://blueskyfeeds.com/en/faq-app-password"
							class="ml-auto inline-block text-sm underline"
							target="_blank"
							rel="noreferrer"
						>
							App Password?
						</a>
					</div>
					<Input
						id="password"
						bind:value={$form.password}
						type="password"
						name="password"
						required
					/>
				</div>
				<LoadingButton submitting={$submitting} cls="w-full" />
				<!-- <Button type="submit" class="w-full" variant="default"> -->
				<!-- 	{#if $submitting} -->
				<!-- 		<LoaderCircle class="animate-spin" /> -->
				<!-- 	{:else} -->
				<!-- 		Login -->
				<!-- 	{/if} -->
				<!-- </Button> -->
			</div>
		</form>
		<div class="mt-4 text-center text-sm">
			Don't have an account?
			<a target="_blank" rel="noreferrer" href="https://bsky.app" class="underline">
				Sign up on Bluesky
			</a>
		</div>
	</Card.Content>
</Card.Root>
