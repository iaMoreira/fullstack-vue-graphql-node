<template>
  <div >
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
          <AppItemList title="Prefixos" v-bind:items="items.prefix" type="prefix" v-on:addItem="addItem" v-on:deleteItem="deleteItem"></AppItemList>
           
          </div>
          <div class="col-md">
            <AppItemList title="Sufixos" v-bind:items="items.sufix" type="sufix" v-on:addItem="addItem" v-on:deleteItem="deleteItem"></AppItemList>

          </div>
        </div>
        <br/>
        <h5>Domínios <span class="badge badge-info">{{domains.length}}</span></h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.id">
                 <div class="row">
                      <div class="col-md-6">
                        {{domain.name}}
                      </div>
                      <div class="col-md-3">
                        <span class="badge badge-info">{{(domain.available) ? "Disponível" : "Não Disponível" }}</span>
                      </div>
                      <div class="col-md text-right">
                        <a class="btn btn-info" v-bind:href=domain.checkout target="_blank" ><span class="fa fa-shopping-cart"></span></a>
                        <button class="btn btn-info" @click="openDomain(domain)">
                          <span class="fa fa-search"></span>
                        </button>
                      </div>
                    </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState, mapActions} from "vuex";
import AppItemList from "./AppItemList";
export default {
  name: "app",
  components: {
    AppItemList
  },
	data: () => ({
		
  }),
  methods: {
   ...mapActions(["addItem", "deleteItem", "getItems", "generateDomains"]),
    openDomain(domain){
      this.$router.push({
        path: `/domains/${domain.name}`
      });
    }

  },
  computed: {
   ...mapState(["items", "domains"])
  },
  
};
</script>
