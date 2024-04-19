<template>
    <div>
        <b-container>
            <b-row>
                <div class="text-center">
                    <h3>Games</h3>
                </div>
            </b-row>
        </b-container>
        <b-alert v-if="error" dismissible variant="danger" @dismissed="error = ''">
            {{ error }}
        </b-alert>

        <b-form-group class="w-25 mb-2">
            <b-form-input v-model="searchQuery" placeholder="Enter search term"></b-form-input>
        </b-form-group>

        <b-table striped bordered :items="filteredGames" :fields="fields" :per-page="perPage" :sort-by.sync="sortBy"
            :sort-desc.sync="sortDesc"></b-table>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            games: [],
            perPage: 100,
            sortBy: "",
            sortDesc: false,
            error: "",
            searchQuery: "",
            fields: [
                { key: "name", label: "Game", sortable: true, sortableIcon: "caret-up-down" },
                { key: "supplier", label: "Producer", sortable: true, sortableIcon: "caret-up-down" },
                { key: "minBet", label: "Min Bet (CHF)", sortable: true, sortableIcon: "caret-up-down" },
                { key: "maxBet", label: "Max Bet (CHF)", sortable: true, sortableIcon: "caret-up-down" },
                { key: "qualificationId", label: "Qualification ID", sortable: true, sortableIcon: "caret-up-down" },
                { key: "version", label: "Game Version", sortable: true, sortableIcon: "caret-up-down" },
            ],
        };
    },
    computed: {
        filteredGames() {
            if (!this.searchQuery) {
                return this.games;
            }
            const search = this.searchQuery.toLowerCase();
            return this.games.filter(game => {
                return Object.values(game).some(value => {
                    return value && value.toString().toLowerCase().includes(search);
                });
            });
        }
    },
    created() {
        this.fetchGames();
    },
    methods: {
        fetchGames() {
            axios
                .get("https://gamelistmiddleware.azurewebsites.net/gamelist")
                .then((response) => {
                    this.games = response.data;
                })
                .catch((error) => {
                    console.error("Error fetching games:", error);
                    this.error = 'Error fetching games: ' + error.message;
                });
        },
    },
};
</script>