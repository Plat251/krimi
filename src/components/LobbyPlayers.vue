<template>
  <v-card class="mt-4">
    <v-slide-y-transition group>
      <v-list-item
        two-line
        v-for="(player, index) in players"
        :key="player.playerkey"
      >
        <v-list-item-content>
          <v-list-item-title class="font-weight-bold">{{
            index + 1 + ". " + player.name
          }}</v-list-item-title>
          <v-list-item-subtitle>
            /game/{{ game.gameId }}/player/{{ player.slug }}
          </v-list-item-subtitle>
        </v-list-item-content>
        <v-list-item-action>
          <v-btn icon @click="makeDetective(index)">
            <v-icon :color="index === active ? 'secondary' : 'gray'"
              >mdi-microscope</v-icon
            >
          </v-btn>
        </v-list-item-action>
      </v-list-item>
    </v-slide-y-transition>
  </v-card>
</template>

<script>
export default {
  props: {
    active: {
	  type: Number,
	  required: true
	},
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
    async makeDetective(player) {
      this.$emit("change", player);;
    }
  }
};
</script>

<style lang="scss" scoped></style>
