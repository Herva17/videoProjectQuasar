<template>
  <div
    style="overflow: auto; width: 30%; border-radius: 6px"
    class="bg-green-1 shadow-10"
  >
    <div
      style="
        width: 200px;
        height: 200px;
        margin-left: auto;
        margin-right: auto;
        margin-top: 10px;
      "
    >
      <q-video
        :src="produit?.image"
        spinner-color="primary"
        spinner-size="82px"
        style="width: 200px; height: 200px; background-color: transparent"
        class="q-ml-auto q-mr-auto"
      />
    </div>
    <div
      class="text-center text-bold text-green q-ml-auto q-mt-lg"
      style="font-size: 170%; text-transform: capitalize"
    >
      {{ produit?.prix }}
    </div>
    <div
      class="text-center text-bold text-white bg-blue-4 q-ml-auto q-mr-auto q-mt-sm"
      style="font-size: 170%; text-transform: capitalize; width: 80%"
    >
      {{ produit?.designation }}
    </div>
    <div class="flex items-center justify-center">
      <div class="">
        <q-btn
          name="favorite"
          icon="favorite"
          color="red-6"
          style="margin-right: 0px"
          flat
          @click="favs(produit?.id)"
        /><span style="margin-left: 0px; color: red">{{ produit?.favs }}</span>
        <q-btn
          name="thumb_up"
          icon="thumb_up"
          color="blue-4"
          style="margin-right: 0px"
          flat
          @click="like(produit?.id)"
        /><span style="margin-left: 0px" class="text-blue-4">{{
          produit?.like
        }}</span>
      </div>
    </div>
    <div class="q-mb-lg flex">
      <q-input
        v-model="comment"
        type="text"
        label="Commentaire"
        class="q-ml-lg q-mr-sm"
      />
      <q-btn
        color="primary"
        label="Envoyer"
        @click="commenter({ id: produit?.id, comment: comment })"
        size="10px"
        style="height: 30px"
      />
    </div>
    <div v-for="(item, index) in produit?.comments" :key="index">
      {{ item }}
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const comment = ref("");
const emits = defineEmits(["updateFav", "updateLike", "commenter"]);
const props = defineProps({
  produit: {
    type: Object,
  },
});
const like = (id) => {
  emits("updateLike", id);
};
const favs = (id) =>{
  emits("updateFav", id);
}
const commenter = (obj) => {
  if (comment.value.length > 0) {
    emits("commenter", { id: obj.id, comment: obj.comment });
    comment.value = "";
  } else {
    alert("entrer un comment");
  }
};
</script>

<style lang="scss" scoped></style>
