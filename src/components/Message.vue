<template>
    <div class="message" v-if="message">
        <p>{{message}}</p>
    </div>
</template>

<script>
export default {
    props: {
       message: {
           type: String,
           required: true
       } 
    }
}
</script>

<style lang="scss" scoped>
    p {
        margin-bottom: 10px;

        text-align: center;
        font-size: 17px;
        font-weight: 500;
        color: rgb(179, 24, 50);
    }
</style>