<script>
	import {
		Page,
		Navbar,
		Button,
		Card,
		CardContent,
		CardHeader,
		Icon,
		List,
		ListItem,
		Link,
		Fab,
		Popup,
		Searchbar,
	} from "framework7-svelte";
	import "skeleton-elements/svelte";

	import DataJson from "./data.json";

	import MdSettings from "../icons/MdSettings.svelte";
	import MdSearch from "../icons/MdSearch.svelte";
	import MdPhone from "../icons/MdPhone.svelte";
	import MdClose from "../icons/MdClose.svelte";
	import MdWhatsapp from "../icons/MdWhatsapp.svelte";
	import MdRoundedSquare from "../icons/MdRoundedSquare.svelte";

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
		<Link
			class="absolute top-0 left-0 pl-2 pt-1"
			href="https://wa.me/+966506906007"
		>
			<Icon>
				<div class="relative">
					<MdWhatsapp
						style="position:absolute; top: 2; left: 2;"
						slot="material"
						class="w-7 h-7"
						fill="white"
					/>
					<MdRoundedSquare
						fill="green"
						style="block"
						slot="material"
						class="w-8 h-8"
					/>
				</div>
			</Icon>
		</Link>
		<img src={ContactBanner} alt="Contact Banner" />
		<Link class="absolute top-0 right-0 pr-2 pt-1" href="tel:+966506906007">
			<Icon>
				<div class="relative">
					<MdPhone
						style="position:absolute; top: 2; left: 2;"
						slot="material"
						class="w-7 h-7"
						fill="white"
					/>
					<MdRoundedSquare
						fill="green"
						style="block"
						slot="material"
						class="w-8 h-8"
					/>
				</div>
			</Icon>
		</Link>
	</div>

	<div
		dir="rtl"
		class="p-4 grid gap-x-4 gap-y-2 grid-cols-2 rtl:space-x-reverse"
	>
		<Card expandable>
			<CardContent padding={false}>
				<div class="bg-color-yellow" style="height: 300px">
					<CardHeader textColor="black" class="display-block">
						Framework7
						<br />
						<small style="opacity: 0.7">Build Mobile Apps</small>
					</CardHeader>
					<Link
						cardClose
						color="black"
						class="card-opened-fade-in"
						style="position: absolute; right: 15px; top: 15px"
						iconF7="xmark_circle_fill"
					/>
				</div>
				<div class="card-content-padding">
					<p>
						Framework7 - is a free and open source HTML mobile framework to
						develop hybrid mobile apps or web apps with iOS or Android
						(Material) native look and feel. It is also an indispensable
						prototyping apps tool to show working app prototype as soon as
						possible in case you need to. Framework7 is created by Vladimir
						Kharlampidi.
					</p>
					<p>
						The main approach of the Framework7 is to give you an opportunity to
						create iOS and Android (Material) apps with HTML, CSS and JavaScript
						easily and clear. Framework7 is full of freedom. It doesn't limit
						your imagination or offer ways of any solutions somehow. Framework7
						gives you freedom!
					</p>
					<p>
						Framework7 is not compatible with all platforms. It is focused only
						on iOS and Android (Material) to bring the best experience and
						simplicity.
					</p>
					<p>
						Framework7 is definitely for you if you decide to build iOS and
						Android hybrid app (Cordova or Capacitor) or web app that looks like
						and feels as great native iOS or Android (Material) apps.
					</p>
					<p>
						<Button fill round large cardClose color="yellow" textColor="black"
							>Close</Button
						>
					</p>
				</div>
			</CardContent>
		</Card>
		{#each mainSections as section}
			<Button link href="/{section}" outline style="padding: 40px;" class="m-1"
				><h1>{section}</h1></Button
			>
		{/each}
	</div>

	<Popup opened={popupOpened} onBackdropClick={() => (popupOpened = false)}>
		<Page>
			<Navbar centerTitle title="البحث">
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
					<Icon>
						<MdClose slot="material" class="w-6 h-6" />
					</Icon>
				</Link>
			</Navbar>
			<List strong insetMaterial outlineIos>
				{#if filteredItems.length === 0}
					<ListItem title="لا توجد بيانات" />
				{/if}
				{#each filteredItems as item (item.title)}
					<ListItem key={item.title} title={item.title} />
				{/each}
			</List>
		</Page>
	</Popup>
</Page>
