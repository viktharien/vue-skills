<template>
    <div class="about">
        <h1>Hello {{ their_name }}</h1>
    </div>
</template>

<script>

    export default {
        name: "About",
        data() {
            return {
                their_name: this.$route.params.name
            }
        },
        methods: {

        }
    }

</script>