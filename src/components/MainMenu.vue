<template lang="">
    <div>
        <nav class="navbar navbar-expand-lg " :style="`background-color: ${color}`">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">{{titulo}}</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                    aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item" v-for="menu in menus" :key="menu.etiqueta">
                            <a class="nav-link" href="#">{{menu.etiqueta}}</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </div>
</template>

<script>
export default {
    name: 'MainMenu',
    props: {
        titulo: {
            type: String
        },
        menus: {
            type: Array
        },
        color: {
            type: String
        }
    }
}
</script>
<style scoped>
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
</style>