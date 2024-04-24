<script>
	import {
		Page,
		Navbar,
		Block,
		Card,
		Button,
		Tabbar,
		TabbarLink,
		NavbarBackLink,
		Icon,
		List,
		ListItem,
		Link,
		Fab,
		Popup,
		Searchbar,
	} from "konsta/svelte";

	import DataJson from "./data.json";

	import MdEmail from "../icons/MdEmail.svelte";
	import MdSettings from "../icons/MdSettings.svelte";
	import MdSearch from "../icons/MdSearch.svelte";
	import MdPhone from "../icons/MdPhone.svelte";
	import MainBanner from "../images/main_banner.jpg";
	import ContactBanner from "../images/contact_banner.jpg";

	let mainSections = [
		"المقدمة",
		"مسائل",
		"محرمات الإحرام",
		"محرمات الحرم",
		"أحكام الكفارة",
		"عمرة التمتع",
		"حج التمتع",
		"الإعلانات",
	];
	let popupOpened = false;
	let searchQuery = "";
	let items = [
		{ title: "FC Ajax" },
		{ title: "FC Arsenal" },
		{ title: "FC Athletic" },
		{ title: "FC Barcelona" },
		{ title: "FC Bayern München" },
		{ title: "FC Bordeaux" },
		{ title: "FC Borussia Dortmund" },
		{ title: "FC Chelsea" },
		{ title: "FC Galatasaray" },
		{ title: "FC Juventus" },
		{ title: "FC Liverpool" },
		{ title: "FC Manchester City" },
		{ title: "FC Manchester United" },
		{ title: "FC Paris Saint-Germain" },
		{ title: "FC Real Madrid" },
		{ title: "FC Tottenham Hotspur" },
		{ title: "FC Valencia" },
		{ title: "FC West Ham United" },
	];

	function handleSearch(e) {
		searchQuery = e.target.value;
	}

	function handleClear() {
		searchQuery = "";
	}

	function handleDisable() {
		console.log("Disable");
	}

	let filteredItems = [];
	/* eslint-disable */
	$: {
		filteredItems = searchQuery
			? items.filter((item) =>
					item.title.toLowerCase().includes(searchQuery.toLowerCase()),
				)
			: items;
	}
</script>

<svelte:head>
	<title>حج التمتع</title>
</svelte:head>

<Page>
	<Fab
		onClick={() => (popupOpened = true)}
		class="fixed right-4-safe bottom-4-safe z-20"
	>
		<svelte:component this={MdSearch} slot="icon" />
	</Fab>
	<div class="relative">
		<Link class="absolute top-0 right-0 p-4" href="#settings">
			<Icon>
				<MdSettings slot="material" class="w-6 h-6" />
			</Icon>
		</Link>

		<img src={MainBanner} alt="Main Banner" />
	</div>
	<div class="relative">
		<Link class="absolute top-0 left-0 p-2" href="https://wa.me/+966506906007">
			<Icon>
				<MdEmail slot="material" class="w-6 h-6" />
			</Icon>
		</Link>
		<img src={ContactBanner} alt="Contact Banner" />
		<Link class="absolute top-0 right-0 p-2">
			<Icon>
				<MdPhone slot="material" class="w-6 h-6" />
			</Icon>
		</Link>
	</div>

	<div
		dir="rtl"
		class="p-4 grid gap-x-4 gap-y-2 grid-cols-2 rtl:space-x-reverse"
	>
		{#each mainSections as section}
			<Button outline><h1>{section}</h1></Button>
		{/each}
	</div>

	<Popup opened={popupOpened} onBackdropClick={() => (popupOpened = false)}>
		<Page>
			<Navbar title="Searchbar">
				<Searchbar
					slot="subnavbar"
					onInput={handleSearch}
					value={searchQuery}
					onClear={handleClear}
					disableButton
					disableButtonText="Cancel"
					onDisable={handleDisable}
				/>
				<Link slot="right" navbar onClick={() => (popupOpened = false)}>
					Close
				</Link>
			</Navbar>
			<List strong insetMaterial outlineIos>
				{#if filteredItems.length === 0}
					<ListItem title="Nothing found" />
				{/if}
				{#each filteredItems as item (item.title)}
					<ListItem key={item.title} title={item.title} />
				{/each}
			</List>
		</Page>
	</Popup>
</Page>
