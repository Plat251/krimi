<template>
  <v-card class="mt-4">
    <v-slide-y-transition group>
      <v-list-item
        v-for="(player, index) in players"
        :key="player.playerkey"
      >
        <v-list-item-content>
          <v-list-item-title class="font-weight-bold">{{
            index + 1 + ". " + player.name
          }}</v-list-item-title>
        </v-list-item-content>
		<v-list-item-action>
            <v-icon v-if="index === active" color="secondary">
				mdi-microscope
			</v-icon>
        </v-list-item-action>
      </v-list-item>
    </v-slide-y-transition>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    active: 0
  }),
  props: {
    players: {
      type: Array,
      required: true
    },
    game: {
      type: Object,
      required: true
    }
  },
  methods: {
    changeDetective(evt) {
      this.active = evt;
    },
  },
  computed: {
	detective() {
		return this.$store.state.game.detective;
	},
  },
  watch: {
	detective() {
		this.active = this.$store.state.game.detective
	},
  },
  async mounted() {
	this.$store.dispatch("loadGame", this.$route.params.id);
	this.changeDetective(this.detective);
    },
  }
</script>

<style lang="scss" scoped></style>
