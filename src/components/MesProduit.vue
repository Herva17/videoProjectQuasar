<template>
  <div
    style="
      width: 250px;
      margin: 20px auto;
      text-align: center;
    "
  >
    <!-- Affichage de l'image principale -->
    <iframe
      :src="produit?.image"
      spinner-color="primary"
      spinner-size="82px"
      style="width: 100%; height: 300px; border-radius: 20px; background-color: transparent;"
      class="q-ml-auto q-mr-auto"
    ></iframe>

    <!-- Boutons d'interaction -->
    <div class="flex items-center justify-center q-mt-md" style="margin-top: -4px;">
      <!-- Bouton pour afficher la carte de commentaires -->
      <q-btn
        name="comment"
        icon="comment"
        color="black"
        flat
        @click="toggleCommentSection"
      />
      <span style="color: black; margin-left: -10px;">{{ produit?.comments.length }}</span>

      <!-- Bouton pour ajouter aux favoris -->
      <q-btn
        name="favorite"
        icon="favorite"
        color="red-6"
        flat
        @click="favs(produit?.id)"
      />
      <span style="color: red; margin-left: -10px;">{{ produit?.favs }}</span>

      <!-- Bouton pour liker -->
      <q-btn
        name="thumb_up"
        icon="thumb_up"
        color="blue-4"
        flat
        @click="like(produit?.id)"
      />
      <span style="margin-left: -10px;">{{ produit?.like }}</span>
    </div>

    <!-- Carte de commentaires, visible uniquement lorsque isCommentSectionVisible est vrai -->
    <q-card
      v-if="isCommentSectionVisible"
      class="q-mt-md"
      style="background: #f8f9fa; padding: 16px; border-radius: 12px;"
    >
      <!-- Section d'ajout d'un commentaire -->
      <div class="flex q-mb-md">
        <q-input
          v-model="comment"
          type="text"
          label="Ajoutez un commentaire"
          class="q-mr-sm"
          dense
          filled
          style="flex: 1;"
        />
        <q-btn
          color="primary"
          icon="send"
          @click="commenter({ id: produit?.id, comment: comment })"
          style="flex-shrink: 0;"
        />
      </div>

      <!-- Liste des commentaires -->
      <div v-if="produit?.comments.length">
        <q-list>
          <q-item v-for="(comment, index) in produit.comments" :key="index" class="q-mb-sm">
            <q-item-section>
              <div style="font-weight: bold;">{{ username }}</div>
              <div>{{ comment }}</div>
            </q-item-section>
          </q-item>
        </q-list>
      </div>
      <div v-else class="text-grey text-center q-mt-sm">Soyez le premier à commenter</div>
    </q-card>
  </div>
</template>




<script setup>
import { ref, defineEmits, defineProps, onMounted } from "vue";

// Déclarations des données réactives
const comment = ref(""); // Stocke le commentaire actuel
const isCommentSectionVisible = ref(false); // Gère la visibilité de la section commentaire
const username = ref(""); // Stocke le nom d'utilisateur

// Déclarations des événements émis au parent
const emits = defineEmits(["updateFav", "updateLike", "commenter"]);

// Déclaration des props reçues du parent
const props = defineProps({
  produit: {
    type: Object, // L'objet produit contient les informations de l'élément (image, favoris, likes, commentaires)
    required: true,
  },
});

// Récupération du nom d'utilisateur depuis le localStorage
onMounted(() => {
  const savedUsername = localStorage.getItem("username");
  if (savedUsername) {
    username.value = savedUsername;
  } else {
    username.value = "Utilisateur par défaut";
  }
});

// Méthode pour liker
const like = (id) => {
  emits("updateLike", id);
};

// Méthode pour ajouter aux favoris
const favs = (id) => {
  emits("updateFav", id);
};

// Méthode pour commenter
const commenter = (obj) => {
  if (comment.value.trim().length > 0) {
    // Émet l'événement avec l'identifiant du produit et le commentaire
    emits("commenter", { id: obj.id, comment: comment.value });
    comment.value = ""; // Réinitialise le champ de commentaire
  } else {
    alert("Veuillez entrer un commentaire."); // Alerte si le champ est vide
  }
};

// Méthode pour afficher/masquer la section de commentaire
const toggleCommentSection = () => {
  isCommentSectionVisible.value = !isCommentSectionVisible.value;
};
</script>


<style lang="scss" scoped></style>
