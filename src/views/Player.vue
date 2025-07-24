<template>
  <v-container style="height:100%" v-if="player && game">
    <v-row
      v-if="!game.started"
      style="height:100%"
      align="center"
      justify="center"
    >
      <v-col cols="12" lg="6">
        <div v-if="!game.started">
          <h2 class="display-2">{{ player.name }}</h2>
          <p class="subtitle-1 my-4">
            {{ t("You are in room") }}
            <code class="accent--text text-uppercase">{{ game.gameId }}</code
            >. {{ t("Waiting for the game start.") }}
          </p>
		  <lobby-players-list
		  :game="game"
          :players="players" />
          <v-progress-linear
            indeterminate
            rounded
            absolute
            bottom
            color="accent"
          ></v-progress-linear>
        </div>
      </v-col>
    </v-row>
    <board v-else-if="game && game.started" />
    <forensic-analysis
      v-if="game.started && player.index === game.detective"
      :game="game"
      :player="player"
    />
    <detective v-else-if="game.started" :game="game" :player="player" />
  </v-container>
</template>

<script>
import LobbyPlayersList from "@/components/LobbyPlayersList";
import ForensicAnalysis from "@/components/ForensicAnalysis";
import Board from "@/components/Board";
import Detective from "@/components/Detective";
export default {
  name: "Player",
  locales: {
    pt_br: {
      "You are in room": "Você está na sala",
      "Waiting for the game start.": "Esperando o jogo começar."
    },
    uk_ua: {
      "You are in room": "Ви у грі",
      "Waiting for the game start.": "Чекаємо на початок гри."
    }
  },
  components: { LobbyPlayersList, ForensicAnalysis, Board, Detective },
  computed: {
    game() {
      return this.$store.state.game;
    },
    player() {
      return this.$store.state.player;
    },
	players() {
      if (!this.game || !this.game.players) return false;
      return Object.keys(this.game.players).map(
        item => this.game.players[item]
      )
	},
  },
  methods: {},
  async mounted() {
    await this.$store.dispatch("loadPlayer", {
      game: this.$route.params.id,
      player: this.$route.params.slug
    });
    this.$translate.setLang(this.game.lang);
  },
  watch: {
    async game(newValue, oldValue) {
      if (oldValue && !oldValue.started && newValue.started) {
        await this.$store.dispatch("loadPlayer", {
          game: this.$route.params.id,
          player: this.$route.params.slug
        });
      }
    }
  }
};
</script>
