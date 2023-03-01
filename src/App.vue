<template>
  <MainMenu :titulo="configuracionPagina.marca" :menus="configuracionPagina.menus"
    :color="configuracionPagina.menuColor" />
  <MainProduct :pedido="pedido" :precioEstilos="configuracionPagina.precioEstilos"
  @increaseQty="increaseQty"
  @decreaseQty="decreaseQty"
  @comprarButton="comprarButton"
    />
  <MainCardList :productos="productos" @selectProduct="selectProduct"/>
  <MainFooter :footerColor="configuracionPagina.footerColor" />
</template>

<script>

//Components
import MainMenu from './components/MainMenu.vue';
import MainProduct from './components/MainProduct.vue'
import MainCardList from './components/MainCardList.vue'
import MainFooter from './components/MainFooter.vue'



export default {
  name: 'App',
  components: {
    MainMenu,
    MainProduct,
    MainCardList,
    MainFooter
  },
  data() {
    return {
      pedido: {
        id: null,
        imagen: null,
        nombre: null,
        descripcion: null,
        precio: null,
        colores: [],
        cantidad: null,
      },
      configuracionPagina:
      {
        marca: "MegaDron",
        menuColor: "lightblue",
        footerColor: "slategrey",
        precioEstilos: "background: orangered; color: white; font-weight: bold",
        menus: [
          {
            etiqueta: "Inicio",
            url: "?"
          },
          {
            etiqueta: "Tienda",
            url: "?"
          }
        ]
      },
      productos: []
    }
  },
  async created() {
    try {
      const response = await this.axios.get('http://localhost:3000/productos');
      this.productos = response.data;
      this.pedido = {
        id: response.data[0].id,
        imagen: response.data[0].imagen,
        nombre: response.data[0].nombre,
        descripcion: response.data[0].descripcion,
        precio: response.data[0].precio,
        colores: response.data[0].colores,
        cantidad: 1,
      };
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    comprarButton(selectedColor) {
      alert(`id: ${this.pedido.id}  - cantidad:  ${this.pedido.cantidad} - color:  ${selectedColor !== null ? selectedColor : this.pedido.colores[0]}`);
    },
    increaseQty() {
      this.pedido.cantidad++;
    },
    decreaseQty() {
      this.pedido.cantidad--;
    },
    selectProduct(pedido) {
      this.pedido = pedido;
      this.configuracionPagina.precioEstilos = `background: ${pedido.colores[0]}; color: white; font-weight: bold`
    },
  },
}
</script>

<style></style>
