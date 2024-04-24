<script>
	import {
		Page,
		Navbar,
		Block,
		Card,
		Button,
		Tabbar,
		TabbarLink,
		Icon,
		Link,
		Fab,
	} from "konsta/svelte";
	import MdEmail from "../icons/MdEmail.svelte";
	import MdSettings from "../icons/MdSettings.svelte";
	import MdHome from "../icons/MdHome.svelte";
	import MdSearch from "../icons/MdSearch.svelte";
	import MainBanner from "../images/main_banner.jpg";
	import ContactBanner from "../images/contact_banner.jpg";

	let activeTab = "tab-1";
	let isTabbarLabels = true;
	let isTabbarIcons = true;
</script>

<svelte:head>
	<title>حج التمتع</title>
</svelte:head>

<Page>
	<Navbar>
		<Link slot="right" navbar
			><Icon>
				<MdSettings slot="material" class="w-6 h-6" />
			</Icon></Link
		>
	</Navbar>
	<Fab class="fixed right-4-safe bottom-4-safe z-20">
		<svelte:component this={MdSearch} slot="icon" />
	</Fab>
	<!-- <Tabbar labels="true" icons="true" class="left-0 bottom-0 fixed">
		<TabbarLink
			active={activeTab === "tab-1"}
			onClick={() => (activeTab = "tab-1")}
			label="الصفحة الرئيسية"
		>
			<svelte:fragment slot="icon">
				<Icon>
					<MdHome
						selected={activeTab === "tab-1"}
						slot="material"
						class="w-6 h-6"
					/>
				</Icon>
			</svelte:fragment>
		</TabbarLink>
		<TabbarLink
			active={activeTab === "tab-2"}
			onClick={() => (activeTab = "tab-2")}
			label="البحث"
		>
			<svelte:fragment slot="icon">
				<Icon>
					<MdSearch slot="material" class="w-6 h-6" />
				</Icon>
			</svelte:fragment>
		</TabbarLink>
	</Tabbar> -->
	<div class="relative">
		<img src={MainBanner} alt="Main Banner" />
		<img src={ContactBanner} alt="Main Banner" />
	</div>

	<div class="p-4 grid gap-x-4 gap-y-2 grid-cols-2 rtl:space-x-reverse">
		{#each [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] as item}
			<Button outline><h1>{item}</h1></Button>
		{/each}
	</div>
</Page>
