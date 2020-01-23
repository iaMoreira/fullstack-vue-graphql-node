<template>
  <div>
    <h5>{{title}} <span class="badge badge-info">{{items.length}}</span> </h5>
		<div class="card">
			<div class="card-body">
				<ul class="list-group">
					<li class="list-group-item" v-for="item in items" v-bind:key="item.di">
						<div class="row">
							<div class="col- md">
								{{item.description}}
							</div>
							<div class="col-md text-right">
								<button class="btn btn-info" v-on:click="deleteItem(item)" ><span class="fa fa-trash"></span></button>
							</div>
						</div>
					</li>
					<br/>
					<div class="input-group">
						<input type="text" class="form-control" v-model="description" v-on:keyup.enter="addItem(type, description)" placeholder="Digite o item"/>
						<div class="input-gruop-append" >
							<button class="btn btn-info" v-on:click="addItem(type, description)"><span class="fa fa-plus"></span></button>
						</div>
					</div>
				</ul>
			</div>
		</div>
  </div>
</template>

<script>
export default {
	name: "AppItemList",
	props: ["title", "items", "type"],
	data: () => ({
		description: "",
	}),
	methods: {
		addItem(type, description){
			this.$emit("addItem", {
				type,
				description
			});
			this.description = "";
		},
		deleteItem(item) {
			this.$emit("deleteItem", item);
		}
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
