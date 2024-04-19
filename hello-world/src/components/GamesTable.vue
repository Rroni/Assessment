<template>
    <div>
        <b-table striped bordered :items="games" :fields="fields" :per-page="perPage" :sort-by.sync="sortBy"
            :sort-desc.sync="sortDesc"></b-table>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            games: [],
            perPage: 10,
            sortBy: '',
            sortDesc: false,
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
                });
        },
    },
};
</script>