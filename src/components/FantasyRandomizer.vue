<template>
  <div class="text-center">
    <v-btn class="text-none text-subtitle-1" color="#F50057" size="small" variant="flat" @click="getRandom">
      Get a random character
    </v-btn>

    <v-card class="mx-auto" max-width="400" v-if="random" style="margin-top: 20px;">
      <div class="text-center">
        <v-img v-if="random && random.pictures && random.pictures.length > 0" :src="random.pictures[0].url" cover
          style="max-width: 200px; max-height: 200px; margin-left: auto; margin-right: auto;">
          <v-card-title></v-card-title>
        </v-img>
      </div>

      <v-card-subtitle class="pt-4">
        {{ random.name }} is your random character
      </v-card-subtitle>

      <v-card-text>
        {{ random.description }}
      </v-card-text>

    </v-card>

    <div>

      <v-card-title class="text-h6 text-md-h5 text-lg-h4">More characters from {{ random.origin }}</v-card-title>

      <v-container>
        <div class="text-center">
          <v-row>
            <v-col v-for="character in filteredCharacters" :key="character.id" cols="12" sm="12" md="9" lg="4">
              <v-card class="mx-auto" :style="{ height: 200}" v-if="random"
                style="margin-top: 20px;">
                <div class="text-center">
                  <v-img height="200" v-if="character && character.pictures && character.pictures.length > 0"
                    :src="character.pictures[0].url" cover
                    style="max-width: 200px; max-height: 200px; margin-left: auto; margin-right: auto;">
                    <v-card-title></v-card-title>
                  </v-img>
                </div>

                <v-card-subtitle class="pt-4">
                  {{ character.name }}
                </v-card-subtitle>

                <v-card-text>
                  {{ truncateDescription(character.description, 43) }}...
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </div>
      </v-container>
    </div>

  </div>
</template>
  
<script>
import axios from 'axios';

export default {

  name: 'FantasyRandomizer',

  mounted() {

    this.getCharacters();

  },
  data() {
    return {
      random: {},
      characters: [],
      filteredCharacters: []
    };
  },


  methods: {
    getCharacters() {
      axios
        .get("https://www.moogleapi.com/api/v1/characters")
        .then(response => {
          this.characters = response.data;
        })
        .catch(error => {
          console.error('Error al obtener los personajes:', error);
        });
    },
    getRandom() {
      axios
        .get("https://www.moogleapi.com/api/v1/characters/random")
        .then(response => {
          this.random = response.data;
          this.filteredCharacters = this.characters.filter(character => character.origin === this.random.origin);
        })
        .catch(error => {
          console.error('Error al obtener el personaje aleatorio:', error);
        });
    },

    truncateDescription(description, wordCount) {
      const words = description.split(' ');

      if (wordCount >= words.length) {
        return description;
      } else {
        const truncatedWords = words.slice(0, wordCount);
        const truncatedDescription = truncatedWords.join(' ');
        return truncatedDescription;
      }
    },
  },

};


</script>

<style>
.text-center {
  margin-top: 20px;
}

.text-h6 {
  justify-content: center;
  display: flex;
}
</style>
  