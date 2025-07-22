<template>
  <v-container style="height:100%">
    <v-row style="height:100%" align="center">
      <v-col class="offset-xl-4" cols="12" lg="6" xl="4">
        <img src="~@/assets/logo.svg" max-width="136" class="mb-4" contain />
        <h2 class="display-2">
          {{ t("A game of") }}
          <vue-typer
            :text="[t('deception'), t('deduction')]"
            erase-style="backspace"
            :type-delay="120"
          />
        </h2>
        <p class="credits">
          {{ t("A web-version of Tobey Ho's") }}
          <strong>Deception: Murder in Hong Kong</strong>.
        </p>
        <p class="subtitle-1 mt-4 mb-10">
          {{
            t(
              "In the game, players take on the roles of investigators attempting to solve a murder case – but there's a twist. The killer is one of the investigators! Find out who among you can cut through deception to find the truth and who is capable of getting away with murder!"
            )
          }}
        </p>
        <div class="d-lg-flex">
          <v-btn
            class="mr-4 mb-4 mb-lg-0"
            type="submit"
            color="grey lighten-5"
            x-large
            to="/join"
            >{{ t("Join game") }}</v-btn
          >
          <v-btn
            class="mr-4 mb-4 mb-lg-0"
            @click.prevent="createNewGame"
            type="submit"
            x-large
            color="accent"
            >{{ t("Create new game") }}</v-btn
          >
        </div>
        <div class="d-lg-flex mt-4">
          <v-btn
            text
            class="mr-4 mb-4 mb-lg-0"
            href="https://medium.com/@raphaelaleixo/krimi-how-to-play-87839028f5ef"
            type="submit"
            target="_blank"
            color="accent"
            >{{ t("How to play") }}</v-btn
          >
          <v-btn
            text
            class="mr-4 mb-4 mb-lg-0"
            href="https://github.com/raphaelaleixo/krimi"
            type="submit"
            target="_blank"
            color="accent"
            >{{ t("About this project") }}</v-btn
          >
          <v-btn
            text
            class="mr-4 mb-4 mb-lg-0"
            @click.prevent="changeLocaleToEN"
            type="submit"
            color="accent"
            >{{ t("English") }}</v-btn
          >
          <v-btn
            text
            class="mr-4 mb-4 mb-lg-0"
            @click.prevent="changeLocaleToPT_BR"
            type="submit"
            color="accent"
            >{{ t("Português ") }}</v-btn
          >
          <v-btn
            text
            class="mr-4 mb-4 mb-lg-0"
            @click.prevent="changeLocaleToUK_UA"
            type="submit"
            color="accent"
            >{{ t("Українська") }}</v-btn
          >
        </div>
        <img
          src="~@/assets/ludoratory.svg"
          max-width="136"
          class="mt-10"
          contain
        />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { VueTyper } from "vue-typer";
export default {
  name: "Home",
  components: { VueTyper },
  methods: {
    async createNewGame() {
      const game = await this.$store.dispatch(
        "createGame",
        this.$translate.lang
      );
      this.$router.push("/game/" + game.gameId);
    },
    changeLocaleToEN() {
      this.$translate.setLang("en");
    },
    changeLocaleToPT_BR() {
      this.$translate.setLang("pt_br");
    },
    changeLocaleToUK_UA() {
      this.$translate.setLang("uk_ua");
    }
  },
  locales: {
    pt_br: {
      "A game of": "Um jogo de",
      deduction: "investigações",
      deception: "intrigas",
      "In the game, players take on the roles of investigators attempting to solve a murder case – but there's a twist. The killer is one of the investigators! Find out who among you can cut through deception to find the truth and who is capable of getting away with murder!":
        "Neste jogo, os jogadores terão o papel de investigadores tentando resolver um caso de assassinato - mas existe um porém. O assassino é um dos investigadores! Descubra quem de vocês pode se livrar das intrigas e achar a verdade e quem é capaz de se safar desta acusação!",
      "About this project": "Sobre este projeto",
      "How to play": "Como jogar",
      "Join game": "Entrar em um jogo",
      "Create new game": "Criar novo jogo",
      "Versão em português": "English version",
      "A web-version of Tobey Ho's": "Uma versão web do jogo de Tobey Ho"
    },
    uk_ua: {
      "A game of": "Гра",
      deduction: "дедукції",
      deception: "обманів",
      "In the game, players take on the roles of investigators attempting to solve a murder case – but there's a twist. The killer is one of the investigators! Find out who among you can cut through deception to find the truth and who is capable of getting away with murder!":
        "У цій грі, гравці беруть на себе ролі слідчих та намагаються розкрити вбивство – але не все так просто. Вбивця - серед них! Дізнайтесь хто з вас зможе розпізнати брехню, а хто може уникнути покарання навіть за вбивство!",
      "About this project": "Про цей проект",
      "How to play": "Як грати",
      "Join game": "Приєднатись до гри",
      "Create new game": "Створити нову гру",
      "Versão em português": "English version",
      "A web-version of Tobey Ho's": "Веб-версія гри Тобі Го"
    }
  }
};
</script>

<style lang="scss">
.vue-typer .custom.char.typed {
  color: #3da9fc;
}
.vue-typer .custom.caret {
  background-color: #094067;
}
.credits {
  margin: 0.5em 0;
  font-size: 1.5em;
}
.vue-typer {
  display: block;
}
</style>
