<template>
    <div>
        <b-container>
            <b-row>
                <!-- Title -->
                <div class="text-center">
                    <h3>Games Catalog</h3>
                </div>
            </b-row>
        </b-container>
        <!-- Error alerts -->
        <ErrorAlert :message="errorMessage" @clear="clearErrorMessage" />
        <!-- Search field -->
        <SearchField :query="searchQuery" @update:query="searchQuery = $event" />
        <!-- Table -->
        <b-table striped bordered :items="filteredGames" :fields="tableFields" :per-page="perPage"
            :current-page="currentPage" :sort-by.sync="sortBy" :sort-desc.sync="sortDesc">
        </b-table>
        <!-- Loader -->
        <div v-if="loading" class="text-center">
            <b-spinner label="Loading..."></b-spinner>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import ErrorAlert from './ErrorAlert.vue';
import SearchField from './SearchField.vue';

export default {
    name: 'GamesTable',
    components: {
        ErrorAlert,
        SearchField
    },

    data() {
        return {
            games: [],
            perPage: 100,
            currentPage: 1,
            sortBy: "",
            sortDesc: false,
            errorMessage: "",
            searchQuery: "",
            loading: false,
            tableFields: [
                { key: "name", label: "Game", sortable: true },
                { key: "supplier", label: "Producer", sortable: true },
                { key: "minBet", label: "Min Bet (CHF)", sortable: true },
                { key: "maxBet", label: "Max Bet (CHF)", sortable: true },
                { key: "qualificationId", label: "Qualification ID", sortable: true },
                { key: "version", label: "Game Version", sortable: true },
            ],
        };
    },

    computed: {
        filteredGames() {
            return this.filterGamesByQuery(this.games, this.searchQuery);
        }
    },

    async created() {
        await this.initiateGameLoading();
    },

    methods: {
        async initiateGameLoading() {
            this.loading = true;
            try {
                const gamesData = await this.fetchGamesDataFromAPI();
                this.updateGamesData(gamesData);
            } catch (error) {
                this.logErrorAndSetMessage(error, "Error fetching games");
            } finally {
                this.loading = false;
            }
        },


        async fetchGamesDataFromAPI() {
            const response = await axios.get("https://gamelistmiddleware.azurewebsites.net/gamelist");
            return response.data;
        },

        updateGamesData(gamesData) {
            this.games = gamesData;
        },

        logErrorAndSetMessage(error, prefixMessage) {
            console.error(`${prefixMessage}:`, error);
            this.errorMessage = `${prefixMessage}: ${error.message}`;
        },

        filterGamesByQuery(games, query) {
            if (!query) return games;
            const normalizedQuery = this.normalizeQuery(query);
            return games.filter(game => this.doesGameMatchQuery(game, normalizedQuery));
        },

        normalizeQuery(query) {
            return query.toLowerCase();
        },

        doesGameMatchQuery(game, normalizedQuery) {
            return Object.values(game).some(value =>
                value && value.toString().toLowerCase().includes(normalizedQuery)
            );
        },

        clearErrorMessage() {
            this.errorMessage = '';
        },
    },
};
</script>
