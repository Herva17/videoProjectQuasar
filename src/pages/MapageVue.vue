<template>
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

  <!-- Ici je vais placer le header -->
</template>

<script setup>
import MesProduit from "src/components/MesProduit.vue";
import { ref } from "vue";
const produits = ref([
  {
    id: 1,
    image:
      "https://th.bing.com/th/id/OIP.ItJeV5ND-4wOKvjLFltmowHaHa?rs=1&pid=ImgDetMain",
    prix: "220 $",
    designation: "Nike",
    favs: 220,
    like: 200,
    comments: ["Ok"],
  },
  {
    id: 2,
    image:
      "https://images-na.ssl-images-amazon.com/images/I/71lbYhyFGYL._AC_UL1200_.jpg",
    prix: "20 $",
    designation: "Budire",
    favs: 2200,
    like: 2400,
    comments: ["Null"],
  },
  {
    id: 4,
    image:
      "https://th.bing.com/th/id/OIP.EGKmq-ZHoLTWm-dzrOHEbgHaHa?pid=ImgDet&w=179&h=179&c=7&dpr=1.5",
    prix: "20 $",
    designation: "Ponch",
    favs: 2200,
    like: 2400,
    comments: ["Bon produit"],
  },
]);
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

<style>
.log {
  font-weight: bolder;
}
</style>
