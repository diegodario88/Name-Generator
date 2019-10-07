<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>NameGator</h1>
      <br />
      <h6 class="text-secndary">Gerador de nomes utilizando Vue.js, GraphQl e Node.</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>
              Prefixos:
              <span class="badge badge-info">{{prefixos.length}}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefixo in prefixos" v-bind:key="prefixo">
                    <div class="row">
                      <div class="col-md">{{ prefixo }}</div>
                      <div class="col-md text-right">
                        <button class="btn btn-danger" v-on:click="deletarPrefixo(prefixo)">
                          <span class="fa fa-trash"></span>
                        </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    class="form-control"
                    type="text"
                    v-model="prefixo"
                    v-on:keyup.enter="addPrefixo(prefixo)"
                    placeholder="Digite o prefixo"
                  />
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefixo(prefixo)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>
              Sufixos:
              <span class="badge badge-info">{{ sufixos.length }}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufixo in sufixos" v-bind:key="sufixo">
                    <div class="row">
                      <div class="col-md">{{ sufixo }}</div>
                      <div class="col-md text-right">
                        <button class="btn btn-danger" v-on:click="deletarSufixo(sufixo)">
                          <span class="fa fa-trash"></span>
                        </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    class="form-control"
                    type="text"
                    v-model="sufixo"
                    placeholder="Digite o sufixo"
                    v-on:keyup.enter="addSufixo(sufixo)"
                  />
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufixo(sufixo)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
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
              <li
                class="list-group-item"
                v-for="dominio in dominios"
                v-bind:key="dominio"
              >{{ dominio }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import { log } from "util";

export default {
  name: "app",
  data: function() {
    return {
      prefixo: "",
      sufixo: "",
      prefixos: ["Air", "Jet", "Flight"],
      sufixos: ["Hub", "Station", "Mart"],
      dominios: [
        "AirHub",
        "AirStation",
        "AirMart",
        "JetHub",
        "JetStation",
        "JetMart",
        "FlightHub",
        "FlightStation",
        "FlightMart"
      ]
    };
  },

  methods: {
    addPrefixo(prefixo) {
      this.prefixos.push(prefixo);
      this.prefixo = "";
      this.generate();
    },
    addSufixo(sufixo) {
      this.sufixos.push(sufixo);
      this.sufixo = "";
      this.generate();
    },
    generate() {
      this.dominios = [];
      this.prefixos.forEach(prefix => {
        this.sufixos.forEach(sufix => {
          this.dominios.push(prefix + sufix);
        });
      });
    },
    deletarPrefixo(prefix) {
      this.prefixos.splice(this.prefixos.indexOf(prefix), 1);
      this.generate();
    },
    deletarSufixo(sufix) {
      this.sufixos.splice(this.sufixos.indexOf(sufix), 1);
      this.generate();
    }
  }
};
</script>

<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}

#main {
  background-image: linear-gradient(to top, #dfe9f3 0%, white 100%);
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>
