<template lang="">
    <div class="container">
        <div class="row">
            <h3>{{pedido.nombre}}</h3>
        </div>
        <div class="row">
            <div class="col-12 col-sm-6 col-md-4 ">
                <img :src="pedido.imagen" :style="{ width: '100%' }">
            </div>

            <div class="col-12 col-sm-6  col-md-8">
                <h6>{{pedido.descripcion}}</h6>
                <div class="p-3 mb-2 text-white" :style="precioEstilos" v-if="selectedColor===null">
                    Precio: {{pedido.precio}} BOB
                </div>
                <div class="p-3 mb-2 text-white" :style="`background: ${selectedColor}; color: white; font-weight: bold`" v-else>
                    Precio: {{pedido.precio}} BOB
                </div>
                <h5>Color</h5>
                <div>
                    <div class="color-box clic" :style="`background: ${color}`" v-for="color in pedido.colores" :key="color" @click="onSelectedColor(color)"></div>
                </div>
                <h5>Cantidad</h5>
                <div class="quantity">
                    <button @click="emitDecreaseQty()">-</button>
                    <div>{{pedido.cantidad}}</div> 
                    <button @click="emitIncreaseQty()">+</button>
                </div>
                <div class="buy-box">
                    <button :disabled="isDisabled" type="button" class="btn btn-primary"
                    @click="emitComprarButton(selectedColor)">Comprar</button>

                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'MainProduct',
    data() {
        return {
            selectedColor: null
        }
    },
    props: {
        pedido: {
            type: Object
        },
        precioEstilos: {
            type: String
        },
    }, 
    methods: {
        emitIncreaseQty() {
            this.$emit('increaseQty');
        },
        emitDecreaseQty() {
            this.$emit('decreaseQty');
        },
        emitComprarButton() {
            this.$emit('comprarButton', this.selectedColor);
        },
        onSelectedColor(color) {
            this.selectedColor = color;
        }
    },
  computed: {
    isDisabled: function () {
      return this.pedido.cantidad < 1 || this.pedido.color === null;
    },
  }
}
</script>
<style scoped>
.color-box {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin: 7px;
    display: inline-block;
}

.clic {
    cursor: pointer;
}

.quantity button {
    border-radius: 50%;
    display: inline-block;
    width: 30px;
}

.quantity div {
    text-align: center;
    min-width: 30px;
    display: inline-block;
    font-weight: bold;
}

.buy-box {
    margin: 20px;
}

.container {
    margin-top: 50px;
}
</style>