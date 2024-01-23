<template>
	<div class="panel panel-left">
		<details v-for="list in lists" :key="list.id" class="details">
			<summary>
				<div class="details__head">
					<div class="checkbox">
						<input type="checkbox" v-model="list.selectedAll" />
						<span
							class="checked"
							:class="[{ 'checked-all': list.selectedAll }, { 'checked-notAll': list.selected }]"
						></span>
					</div>
					<span class="label">{{ list.name }}</span>
				</div>
			</summary>
			<ul class="details__list">
				<li v-for="(item, index) in list.items" :key="index" class="details__list_item">
					<div class="details__list_item_inner details__list_item_inner-left">
						<div class="checkbox">
							<input type="checkbox" v-model="item.selected" />
							<span class="checked checked-all"></span>
						</div>
						<span class="label">{{ item.name }}</span>
					</div>
					<div class="details__list_item_inner details__list_item_inner-right">
						<input type="number" v-model="item.quantity" class="innerInput quantity" />
						<input type="color" v-model="item.color" class="innerInput color" />
					</div>
				</li>
			</ul>
		</details>
	</div>
</template>

<script setup>
const props = defineProps({
	lists: Array,
});

const emit = defineEmits(["updateSelectedItems", "itemIsSelected"]);

const updateSelectedItems = (id) => {
	emit("updateSelectedItems", id);
};
const itemIsSelected = (id) => {
	emit("itemIsSelected", id);
};
</script>

<style lang="scss" scoped>
.details {
	&:not(:last-child) {
		margin-bottom: 10px;
	}
	summary {
		cursor: pointer;
	}
	&__head {
		display: inline-flex;
		align-items: center;
		gap: 5px;
	}
	&__list {
		display: flex;
		flex-direction: column;
		gap: 10px;
		padding-left: 30px;
		&_item {
			display: flex;
			align-items: center;
			width: 100%;
			justify-content: space-between;
			gap: 30px;
			&_inner {
				display: flex;
				align-items: center;
				gap: 10px;
				.innerInput {
					width: 30px;
					height: 30px;
					font-size: 0.8rem;
					border: 1px solid transparent;
					outline: none;
					text-align: center;
					cursor: pointer;
				}
				.quantity {
					&:focus {
						border-color: #000;
					}
					&::-webkit-outer-spin-button,
					&::-webkit-inner-spin-button {
						-webkit-appearance: none;
					}
				}
				.color {
					background: none;
					border: none;
				}
			}
		}
	}
}
</style>
