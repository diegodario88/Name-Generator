<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>NameGator</h1>
      <br />
      <h6 class="text-secndary">Gerador de nomes utilizando Vue.js, GraphQl e Node.</h6>
    </div>
    <div id="main">
      <DomainList />
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import DomainList from "./components/DomainList";

export default {
  name: "app",
  components: {
    DomainList
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
