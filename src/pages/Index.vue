<template>
  <q-page class="flex flex-center">
     
        <q-img src="https://i.ytimg.com/vi/ixMwsbdV6F8/maxresdefault.jpg" 
        style="height: 170px;">
          <div class="absolute-full text-h2 text-bold flex flex-center">
             Menu
          </div>
        </q-img>
     
    <div class="row justify-center container q-px-lg">

      <div
        class="col-12 col-sm-6 col-md-4 col-lg-3 q-pa-md"
        v-for="(pizza, index) in variedades"
        :key="index"
      >
        <q-card class="my-card" flat bordered>
          <div>
            <q-img :src="pizza.imagen" :ratio="4 / 3" />

            <q-badge color="orange" floating class="text-body1"
              >${{ pizza.precio }} c/u</q-badge
            >
          </div>
          <q-card-section class="q-pa-sm">
            <div class="text-h5 ">{{ pizza.nombre }}</div>
            <div class="text-caption text-grey">
              {{ pizza.ingredientes }}
            </div>
          </q-card-section>

          <q-card-actions class="relative-position">
            <q-btn round color="secondary" icon="add" @click="aumentar(index)" />
            <div class="text-h5 q-mx-md">{{ pizza.cantidad }}</div>
            <q-btn
              round
              color="red"
              icon="remove"
              @click="reducir(index)"
            />
            <div
              class="text-h5 q-mr-md q-mt-md  absolute-right absolute-botton"
            >
              ${{ pizza.precio * pizza.cantidad }}
            </div>
          </q-card-actions>
        </q-card>
      </div>
    </div>
    <div class="row justify-center q-py-xl">
      <div class="col-12   text-center items-center">
        <q-btn
          color="primary"
          icon="store"
          label="Realizar Pedido"
          size="xl"
          @click="pedido"
        />
      </div>
    </div>
    <q-dialog
      v-model="persistent"
      persistent
      transition-show="scale"
      transition-hide="scale"
    >
      <q-card class="bg-primary text-white" style="width: 100%">
        <q-card-section>
          <div class="text-h6">Confirmar Pedido</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="row justify-center" v-for="(item, index) in pedidos" :key="index">
            <div class="col-6">{{ item.nombre }} </div>
            <div class="col-1">X </div>
            <div class="col-1">{{ item.cantidad }}</div>

            <div class="col-1 text-center">
              =
            </div>
            <div class="col-3">${{ item.precio * item.cantidad }}</div>
          </div>
          <br>
          <div class="col">
            total = ${{totalFinal}}
            </div>
          
        </q-card-section>

        <q-card-actions align="right" class="bg-white text-orange">
       
       
        <q-btn flat label="Confirmar" v-close-popup @click="confirmar" />

       
          <q-btn flat label="Cancelar" v-close-popup @click="cancelar" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      total:0,
      mensaje:"Hola%20,quiero%20",
      telefono:543624597140,
      pedidos: [],
      variedades: [
        {
          nombre: "Pizza Comun",
          ingredientes: "Salsa, Queso Cremoso, Huevo, Aceituna y Morron",
          precio: 250,
          cantidad: 0,
          imagen: "https://i.ibb.co/jM01yrS/comun.jpg"
        },
        {
          nombre: "Pizza Especial",
          ingredientes: "Salsa, Queso Cremoso, Huevo, Aceituna, Morron y Jamon",
          precio: 300,
          cantidad: 0,
          imagen: "https://i.ibb.co/HBMNhYh/especial.jpg"
        },
        {
          nombre: "Pizza Muzarella",
          ingredientes: "Salsa, Queso Muzarella, Huevo, Aceituna, Morron.",
          precio: 300,
          cantidad: 0,
          imagen: "https://i.ibb.co/wSrpNzD/muzzarella.jpg"
        },
        {
          nombre: "Pizza Especial Muzarella",
          ingredientes:
            "Salsa, Queso Cremoso, Huevo, Aceituna, Morron y Jamon.",
          precio: 350,
          cantidad: 0,
          imagen: "https://i.ibb.co/tK3TqnX/IMG-20210102-235551640.jpg"
        },
        {
          nombre: "Pizza Napolitana",
          ingredientes:
            "Salsa, Queso Muzarella, Huevo, Aceituna, Morron y Tomete.",
          precio: 350,
          cantidad: 0,
          imagen: "https://i.ibb.co/st2Hqzd/napolitana.jpg"
        },
        {
          nombre: "Pizza Calabresa",
          ingredientes: "Salsa, Queso Muzzarella, Salame, Aceituna.",
          precio: 350,
          cantidad: 0,
          imagen: "https://i.ibb.co/W5tTvP1/IMG-20210102-WA0008.jpg"
        }
      ],
      persistent: false
    };
  },
  methods: {
    aumentar(index) {
      this.variedades[index].cantidad += 1;
    },
    reducir(index) {
      if (this.variedades[index].cantidad > 0) {
        this.variedades[index].cantidad -= 1;
      }
    },
    pedido() {
      this.variedades.forEach(element => {
        if (element.cantidad > 0) {
          this.pedidos.push(element);
        }
      });
      this.persistent = true;

    },
    cancelar() {
      this.pedidos = [];
      this.total=0;
    },
    confirmar(){

      this.pedidos.forEach(elemento=>{

        this.mensaje += elemento.cantidad+"%20"+elemento.nombre+"%20"+"+"

      })
      window.location.assign(`https://api.whatsapp.com/send?phone=${this.telefono}&text=${this.mensaje}`);
    this.mensaje = "Hola%20,quiero%20";
    this.pedidos = [];
      this.total=0;
    }
    
  },
  computed:{
    totalFinal: function(){
    this.pedidos.forEach(pizza=>{
      this.total += pizza.cantidad * pizza.precio;
    })
  return this.total
  }}
};
</script>
