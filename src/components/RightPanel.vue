<template>
	<div class="panel panel-right">
		<details class="details" v-for="list in lists" :key="list.id">
			<summary>
				<div class="details__head">{{ list.name }}</div>
			</summary>
			<div class="details__wrapper">
				<template v-for="item in list.items" :key="item.id">
					<ul class="details__list" v-if="item.selected">
						<li
							class="details__list_item"
							v-for="squeare in item.quantity"
							:style="{ background: item.color }"
							:key="squeare"
						></li>
					</ul>
				</template>
			</div>
		</details>
	</div>
</template>

<script>
import { ref, watch } from "vue";

export default {
	name: "RightPanel",
	props: {
		lists: Array,
	},
	setup(props, { emit }) {
		const decreaseQuantity = (selectedItem) => {
			selectedItem.quantity--;
			emit("decreaseQuantity", selectedItem);
		};

		watch(
			() => props.selectedItems,
			() => {
				// Может потребоваться обработка изменений в выбранных элементах
			}
		);

		return {
			decreaseQuantity,
		};
	},
};
</script>

<!-- Стили могут быть добавлены в отдельные файлы -->
<style scoped lang="scss">
.details {
	display: flex;
	flex-direction: column;
	gap: 20px;
	border-radius: 5px;
	border: 1px solid #ccc;
	&::-webkit-details-marker {
		display: none;
	}
	&:not(:last-child) {
		margin-bottom: 20px;
	}
	summary {
		padding: 10px;
		list-style: none;
		cursor: pointer;
	}
	&__wrapper {
		display: flex;
		flex-direction: column;
		gap: 10px;
		padding: 10px;
	}
	&__head {
		display: inline-flex;
	}
	&__list {
		display: flex;
		align-items: center;
		flex-wrap: wrap;
		gap: 5px;
		&_item {
			width: 20px;
			height: 20px;
		}
	}
}
</style>
