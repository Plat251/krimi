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
        </v-list-item-content>
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
  }
};
</script>

<style lang="scss" scoped></style>
