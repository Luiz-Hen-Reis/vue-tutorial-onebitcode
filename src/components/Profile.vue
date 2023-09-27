<script setup>
import { computed, onMounted, onUnmounted, onUpdated, reactive } from "vue";
import UserInfo from "./UserInfo.vue";
import Repository from "./Repository.vue";
import Form from "./Form.vue";

const state = reactive({
  login: "",
  name: "",
  bio: "",
  company: "",
  avatar_url: "",
  repos: [],
});

async function fetchGithubUser(username) {
  const res = await fetch(`https://api.github.com/users/${username}`);
  const { login, name, bio, company, avatar_url } = await res.json();

  state.login = login;
  state.name = name;
  state.bio = bio;
  state.company = company;
  state.avatar_url = avatar_url;

  fetchUserRepositories(login);
}

async function fetchUserRepositories(username) {
  const res = await fetch(`https://api.github.com/users/${username}/repos`);
  const repos = await res.json();

  state.repos = repos;
}

const countReposMessage = computed(() => {
  return state.repos.length > 0
    ? `${state.name} possui ${state.repos.length} repositórios públicos.`
    : `${state.name} não possui nenhum repositório público.`;
});

onMounted(() => console.log("O componente foi montado"));
onUpdated(() => console.log("O componente foi atualizado"));
onUnmounted(() => console.log("O componente foi desmontado"));
</script>

<template>
  <slot></slot>
  <Form @form-submit="fetchGithubUser" />

  <UserInfo
    v-if="state.login !== ''"
    :avatar_url="state.avatar_url"
    :name="state.name"
    :bio="state.bio"
    :company="state.company"
    :login="state.login"
  />

  <section v-if="state.repos.length > 0">
    <h2>{{ countReposMessage }}</h2>

    <Repository
      v-for="repo of state.repos"
      :full_name="repo.full_name"
      :description="repo.description"
      :html_url="repo.html_url"
    />
  </section>

  <slot name="footer"></slot>
</template>
