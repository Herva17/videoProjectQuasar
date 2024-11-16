<template>
  <q-page class="flex flex-center">
    <q-card class="q-pa-md" style="width: 400px">
      <q-card-section>
        <div class="text-h6">Connexion</div>
        <div class="text-subtitle2">Veuillez vous connecter à votre compte</div>
      </q-card-section>

      <q-card-section>
        <q-form @submit.prevent="loginUser">
          <q-input
            v-model="email"
            type="email"
            label="Email"
            hint="Entrez votre adresse email"
            dense
            filled
            class="q-mb-md"
          />
          <q-input
            v-model="password"
            type="password"
            label="Mot de passe"
            dense
            filled
            class="q-mb-md"
          />
          <q-btn
            label="Se connecter"
            type="submit"
            color="primary"
            class="full-width"
          />
        </q-form>
      </q-card-section>

      <q-card-actions align="center">
        <q-btn flat label="Mot de passe oublié ?" color="primary" />
      </q-card-actions>
    </q-card>
  </q-page>
</template>

<script>
import { ref } from "vue";

export default {
  name: "LoginPage",
  setup(_, { root }) {
    // Liste des utilisateurs enregistrés en local
    const users = ref([
      { id: 1, nom: "iragi", email: "iragi@example.com", password: "12345" },
      { id: 2, nom: "john", email: "john@example.com", password: "password" },
    ]);

    // Champs du formulaire
    const email = ref("");
    const password = ref("");

    // Méthode de connexion
    const loginUser = () => {
      const user = users.value.find(
        (u) => u.email === email.value && u.password === password.value
      );

      if (user) {
        console.log("User Logged In:", user.nom);
        alert(`Bienvenue, ${user.nom}!`);
        this.$router.push({ name: 'login', query: { redirect: '/MapageVue.vue' } });
      } else {
        console.log("Invalid Credentials");
        alert("Identifiants incorrects. Veuillez réessayer.");
      }
    };

    return {
      email,
      password,
      loginUser,
    };
  },
};
</script>

<style scoped>
.full-width {
  width: 100%;
}
</style>
