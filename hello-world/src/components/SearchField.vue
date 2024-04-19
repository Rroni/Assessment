<template>
    <b-form-group label="Search Games" label-for="search-input" class="mb-2" label-cols-sm="3" label-align-sm="right"
        align="center">
        <b-form-input id="search-input" v-model="localQuery" placeholder="Enter search term"
            @input="updateQuery"></b-form-input>
    </b-form-group>
</template>

<script>
export default {
    name: 'SearchField',
    props: {
        query: String
    },
    data() {
        return {
            localQuery: this.query
        };
    },
    methods: {
        updateQuery() {
            this.$emit('update:query', this.localQuery);
        }
    },
    watch: {
        query(newVal) {
            this.localQuery = newVal;
        }
    }
};
</script>
