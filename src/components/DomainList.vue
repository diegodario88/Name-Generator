<template>
  <div class="container">
    <div class="row">
      <div class="col-md">
        <ItemListComponent
          title="Prefixo"
          v-bind:items="prefixos"
          v-on:addItem="addPrefixo"
          v-on:deletarItem="deletarPrefixo"
        ></ItemListComponent>
      </div>
      <div class="col-md">
        <ItemListComponent
          title="Sufixo"
          v-bind:items="sufixos"
          v-on:addItem="addSufixo"
          v-on:deletarItem="deletarSufixo"
        ></ItemListComponent>
      </div>
    </div>
    <br />
    <h5>
      Domínios
      <span class="badge badge-info">{{ dominios.length }}</span>
    </h5>
    <div class="card">
      <div class="card-body">
        <ul class="list-group">
          <li class="list-group-item" v-for="dominio in dominios" v-bind:key="dominio.name">
            <div class="row">
              <div class="col-md">{{ dominio.name }}</div>
              <div class="col-md text-right">
                <a class="btn btn-info" v-bind:href="dominio.checkout" target="_blank">
                  <i class="fa fa-shopping-cart" aria-hidden="true"></i>
                </a>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import ItemListComponent from "./ItemListComponent";

export default {
  name: "DomainList",
  components: {
    ItemListComponent
  },
  data: function() {
    return {
      prefixos: ["Air", "Jet", "Flight"],
      sufixos: ["Hub", "Station", "Mart"]
    };
  },

  methods: {
    addPrefixo(prefixo) {
      this.prefixos.push(prefixo);
    },
    addSufixo(sufixo) {
      this.sufixos.push(sufixo);
    },

    deletarPrefixo(prefix) {
      this.prefixos.splice(this.prefixos.indexOf(prefix), 1);
    },
    deletarSufixo(sufix) {
      this.sufixos.splice(this.sufixos.indexOf(sufix), 1);
    }
  },
  computed: {
    dominios() {
      const domains = [];
      this.prefixos.forEach(prefix => {
        this.sufixos.forEach(sufix => {
          const name = prefix + sufix;
          const url = name.toLocaleLowerCase();
          const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;
          domains.push({
            name,
            checkout
          });
        });
      });
      return domains;
    }
  }
};
</script>

<style>
</style>
