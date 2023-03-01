<template lang="">
    <div class="container ">
        <div class="row">
            <h4>Productos relacionados</h4>
        </div>
        <div class="row">
            <div class="col" v-for="producto in productos" :key="producto.id">
                <div class="card" style="width: 18rem;">
                    <div class="card-body clic" @click="onSelectProduct(producto)">
                        <h5 class="card-title">{{ producto.nombre }}</h5>
                        <img :src="producto.imagen" :style="{ width: '100%' }">
                        <p class="card-text">{{producto.descripcion}}</p>
                        <div class="producto-relacionado-precio">Precio:{{producto.precio}} BOB</div>
                        <div>
                            <div>
                                <div class="color-box" :style="`background: ${color}`" v-for="color in producto.colores" :key="color"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'MainCardList',
    data() {
        return {
            selectedColor: null,
            pedido: {
                id: null,
                imagen: null,
                nombre: null,
                descripcion: null,
                precio: null,
                colores: [],
                cantidad: null,
            }
        }
    },
    props: {
        productos: {
            type: Array,
            required: true
        }
    },
    methods: {
        onSelectProduct(producto) {
            const pd = {
                id: producto.id,
                imagen: producto.imagen,
                nombre: producto.nombre,
                descripcion: producto.descripcion,
                precio: producto.precio,
                colores: producto.colores,
                cantidad: 1,
            }
            this.pedido = pd;
            this.$emit('selectProduct', this.pedido);
        }
    }
}
</script>
<style scoped>
.clic {
    cursor: pointer;
}

.color-box {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin: 7px;
    display: inline-block;
}

.quantity div {
    text-align: center;
    min-width: 30px;
    display: inline-block;
    font-weight: bold;
}

.container {
    margin-top: 50px;
}

.producto-relacionado-precio {
    background: orangered;
    color: white;
    text-align: center;
    padding: 10px;
}
</style>