<template>
   <q-header elevated>
      <q-toolbar class="bg-green">
        <q-toolbar-title class="text-center"> Gestion video </q-toolbar-title>
      </q-toolbar>
    </q-header>
  <div class="q-gutter-lg q-pa-sm row">
    <MesProduit
      :produit="item"
      v-for="(item, index) in produits"
      :key="index"
      @updateLike="(id) => updateLike(id)"
      @updateFav="(id) => updateFav(id)"
      @commenter="(obj) => commenter(obj)"
    />
  </div>



</template>

<script setup>
import MesProduit from "src/components/MesProduit.vue";
import { ref } from "vue";
const produits = ref([
  {
    id: 1,
    image:
      "https://www.youtube.com/embed/WU2kVU4TyrE",
    favs:0,
    like: 0,
    comments: [],
  },
  {
    id: 2,
    image:
      "https://www.youtube.com/embed/lGyWMsXel2U",
    favs: 0,
    like: 0,
    comments: [],
  },
  {
    id: 4,
    image:
      "https://www.youtube.com/embed/WU2kVU4TyrE",
    favs: 0,
    like: 0,
    comments: [],
  },
]);

const username = ref(""); // Pour stocker le nom de l'utilisateur connecté


const updateLike = (id) => {
  produits.value.find((el) => el.id === id).like++;
};

const updateFav = (id) => {
  produits.value.find((el) => el.id === id).favs++;
};

const commenter = (obj) => {
  produits.value.find((el) => el.id === obj.id).comments.push(obj.comment);
};
</script>

<style scoped>
.log {
  font-weight: bolder;
}
</style>
