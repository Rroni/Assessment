<template>
    <b-alert v-if="message" variant="danger" dismissible @dismissed="clearMessage">
        {{ message }}
    </b-alert>
</template>

<script>
export default {
    name: 'ErrorAlert',
    props: {
        message: String
    },
    methods: {
        clearMessage() {
            this.$emit('clear');
        }
    }
};
</script>
