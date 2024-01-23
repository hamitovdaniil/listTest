<template>
	<main id="app">
		<LeftPanel :lists="lists" />
		<RightPanel :lists="lists" />
	</main>
</template>

<script setup>
import { ref, onMounted, watch, watchEffect } from "vue";
import LeftPanel from "./components/LeftPanel.vue";
import RightPanel from "./components/RightPanel.vue";

const getRandom = (min, max) => {
	return Math.floor(Math.random() * (max - min) + min);
};

const getRandomColor = () => {
	var letters = "0123456789ABCDEF";
	var color = "#";
	for (var i = 0; i < 6; i++) {
		color += letters[Math.floor(Math.random() * 16)];
	}
	return color;
};

const lists = ref([
	{
		id: 1,
		name: "List 1",
		selected: false,
		selectedAll: false,
		items: [],
	},
	{
		id: 2,
		name: "List 2",
		selected: false,
		selectedAll: false,
		items: [],
	},
	{
		id: 3,
		name: "List 3",
		selected: false,
		selectedAll: false,
		items: [],
	},
	{
		id: 4,
		name: "List 4",
		selected: false,
		selectedAll: false,
		items: [],
	},
	{
		id: 5,
		name: "List 5",
		selected: false,
		selectedAll: false,
		items: [],
	},
]);

function getRandomItems() {
	lists.value.forEach((list) => {
		for (let i = 0; i < getRandom(4, 10); i++) {
			list.items.push({
				id: list.items.length + 1,
				name: `Item ${list.items.length + 1}`,
				quantity: getRandom(1, 10),
				color: getRandomColor(),
				selected: false,
			});
		}
	});
}
getRandomItems();

watchEffect(() => {
	lists.value.forEach((list) => {
		if (list.selectedAll) {
			list.items.forEach((item) => {
				item.selected = true;
			});
		} else {
			list.items.forEach((item) => {
				item.selected = false;
			});
		}
		list.items.forEach((item) => {
			if (item.selected) {
				list.selected = true;
			}
		})
	});
});
</script>

<style lang="scss">
main {
	padding: 30px;
	display: flex;
	gap: 30px;
}

.panel {
	width: calc(50% - 15px);
}
</style>
