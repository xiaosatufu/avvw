<template>
	<div>
		<div>
			<span class="ccc">111222</span>
		</div>
		<Search placeholder="Search here"/>
		<List v-model="loading" :finished="finished" finished-text="no more..." @load="loadMore">
			<Cell v-for="item in list" :key="item" :title="item"/>
		</List>
	</div>
</template>

<script>
	import { Search, List, Cell } from "vant";

	window.tab4Vue = {
		name: "tab1",
		components: { Search, List, Cell },
		data() {
			return {
				list: [],
				loading: false,
				finished: false
			};
		},
		methods: {
			loadMore() {
				// async load datas
				setTimeout(() => {
					for (let i = 0; i < 10; i++) {
						this.list.push(this.list.length + i);
					}

					this.loading = false;

					if (this.list.length > 40) {
						this.finished = true;
					}
				}, 0);
			}
		}
	};

	export default window.tab4Vue;
</script>

<style scoped lang="scss">
div {
	.ccc {
		color: red;
		display: flex;
	}
}
</style>