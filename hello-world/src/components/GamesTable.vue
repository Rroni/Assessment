<template>
    <div>
        <b-table striped bordered head-variant="dark" :items="games" :fields="fields" :per-page="perPage"></b-table>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name: "GamesTable",
    created() {
        this.fetchGames();
    },
    data() {
        return {
            games: [],
            perPage: 100,
            fields: [
                { key: "name", label: "Game" },
                { key: "supplier", label: "Producer" },
                { key: "minBet", label: "Min Bet (CHF)" },
                { key: "maxBet", label: "Max Bet (CHF)" },
                { key: "qualificationId", label: "Qualification ID" },
                { key: "version", label: "Game Version" },
            ],
        };
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