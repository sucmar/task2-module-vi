<template lang="">
    <div>
        <footer :style="`background-color: ${footerColor}`">
        </footer>
    </div>
</template>
<script>
export default {
    name: 'MainFooter',
    props: {
        footerColor: {
            type: String
        }
    }
}
</script>
<style scoped>
footer {
    text-align: center;
    padding: 30px 10px;
    margin-top: 50px;
    min-height: 100px;
}
</style>