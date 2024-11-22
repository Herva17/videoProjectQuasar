<template>
  <q-page class="flex flex-center">
    <q-card class="q-pa-md" style="width: 400px">
      <q-card-section>
        <div class="text-h6">Connexion</div>
        <div class="text-subtitle2">Veuillez vous connecter à votre compte</div>
      </q-card-section>

      <q-card-section>
        <q-form @submit="loginUser">
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
import { useRouter } from "vue-router"; // Importe useRouter

export default {
  name: "MapageVue",
  setup() {
    const router = useRouter(); // Accède au routeur
    const users = ref([
      { id: 1, nom: "iragi", email: "iragi@example.com", password: "12345" },
      { id: 2, nom: "john", email: "john@example.com", password: "password" },
    ]);

    const email = ref("");
    const password = ref("");

    const loginUser = () => {
      const user = users.value.find(
        (u) => u.email === email.value && u.password === password.value
      );

      if (user) {
        console.log("User Logged In:", user.nom);
        alert(`Bienvenue, ${user.nom}!`);

        // Stocker le nom de l'utilisateur dans Local Storage
        localStorage.setItem("username", user.nom);

        // Redirige vers la page d'accueil après connexion réussie
        router.push("/MaPage");
      } else {
        console.log("Identifiants incorrects");
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
