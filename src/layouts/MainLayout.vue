<template>
  <q-layout view="hhh lpR fff">
    <q-header elevated prominent class="bg-yellow text-white q-py-sm">
      <q-toolbar >
        <q-toolbar-title class="text-center">
          <q-avatar>
            <img src="https://tresenlavapies.com/images/icon-pizza.png" />
          </q-avatar>
          <span class="text-bold text-grey-8 q-ml-md ">Pizzas Ta-Ni-Na</span>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>




    <q-page-container class="bg-grey-4">
      <router-view />
    </q-page-container>

    <q-footer  class="bg-orange text-white">
      <q-toolbar>

        <div class="text-center ">
      <p>Desarrolado por Pedroso Nahuel Nicolas  Tel.: 3624784315</p>
</div>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
export default {
  name: "MainLayout",
  data() {
    return {


    };
  }
};
</script>

