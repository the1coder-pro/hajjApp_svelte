<script lang="ts">
	import { page } from "$app/stores";
	// import { Page, NavbarBackLink, Navbar } from "konsta/svelte";

	import {
		Page,
		Navbar,
		Card,
		Link,
		Button,
		CardHeader,
		CardContent,
	} from "framework7-svelte";
	import { onMount } from "svelte";
	/** @type {import('./$types').PageData} */
	let json = JSON.parse(JSON.stringify($page, null, 2));
	let pageTitle = json.params.slug;

	let data = [];
	if (pageTitle == "الإعلانات") {
		const url =
			"https://opensheet.elk.sh/1IR-c-DM1_G0Qr6sr-iy7gZKwWN5zuQfo_Vr8Ky29BgE/1";

		onMount(async function () {
			const response = await fetch(url);
			data = await response.json();
		});
		console.log(data);
	}

	// get id from google drive image link "https://drive.google.com/open?id="
	function getDriveId(url) {
		const id = url.split("id=")[1];
		return id;
	}

	// google drive working images link
	// 1st working link = https://drive.google.com/thumbnail?id=1qKB6GcdeBZ7hY4xxoPGum_VNPJcJayVH&sz=w1000;
	// id =  1qKB6GcdeBZ7hY4xxoPGum_VNPJcJayVH
	// 2nd working link = https://lh3.googleusercontent.com/d/1qKB6GcdeBZ7hY4xxoPGum_VNPJcJayVH;
</script>

<Page>
	<Navbar title={pageTitle} backLink="Back"></Navbar>

	{#if pageTitle == "الإعلانات"}
		{#if data.length > 0}
			{#each data as item}
				<Card expandable>
					<CardContent padding={false}>
						<div
							style="background: url({`https://drive.google.com/thumbnail?id=${getDriveId(item.Image)}`}) no-repeat center top; background-size: cover; height: 400px"
						>
							<CardHeader textColor="white">{item.Title}</CardHeader>
							<Link
								cardClose
								color="white"
								class="card-opened-fade-in"
								style="position: absolute; right: 15px; top: 15px"
								iconF7="xmark_circle_fill"
							/>
						</div>
						<div class="card-content-padding">
							<p>
								{item.Description}
							</p>
							<!-- button for link -->
							<Button fill round large href={item.Link}>Go to Link</Button>
							<p>
								<Button fill round large cardClose>Close</Button>
							</p>
						</div>
					</CardContent>
				</Card>
			{/each}
		{:else}
			<h3>Loading...</h3>
		{/if}
	{:else}
		<h3>{pageTitle}</h3>
	{/if}
</Page>
