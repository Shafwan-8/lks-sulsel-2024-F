<!-- @format -->

<script setup>
import { RouterLink, RouterView, useRouter } from 'vue-router'
import { ref, onMounted } from 'vue';
import Cookies from 'js-cookie';
import Api from '../api'

const router = useRouter();
const isLoggedIn = ref(false);

const checkLoginStatus = () => {
    isLoggedIn.value = !!Cookies.get('token');
};

const logout = async () => {
    try {
        // Get the token from cookies
        const token = Cookies.get('token');

        // Send a request to the backend to delete the token
        await Api.post('/logout', {}, {
            headers: {
                'Authorization': `Bearer ${token}`
            }
        });
    } catch (error) {
        console.error('Failed to logout from backend:', error);
    }

    // Remove the token from cookies
    Cookies.remove('token');
    isLoggedIn.value = false;
    router.push({ name: 'login' });
};

onMounted(() => {
    checkLoginStatus();
});
</script>

<template lang="">
  <header>
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark mb-5">
      <div class="container-lg">
        <a class="navbar-brand" href="#">WS</a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarCollapse"
          aria-controls="navbarCollapse"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarCollapse">
          <ul class="navbar-nav mr-auto mb-2 mb-md-0">
            <li class="nav-item">
              <a class="nav-link" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                List
              </a>
              <ul class="dropdown-menu">
                <li>
                  <RouterLink
                    class="dropdown-item"
                    :to="{ name: 'destinations' }"
                    >Destinations</RouterLink
                  >
                </li>
                <li>
                  <RouterLink class="dropdown-item" :to="{ name: 'events' }"
                    >Events</RouterLink
                  >
                </li>
                <li>
                  <RouterLink class="dropdown-item" :to="{ name: 'posts' }"
                    >Posts</RouterLink
                  >
                </li>
                <li>
                  <RouterLink class="dropdown-item" :to="{ name: 'galleries' }"
                    >Galleries</RouterLink
                  >
                </li>
              </ul>
            </li>
          </ul>
          <div class="me-auto"></div>
          <template v-if="isLoggedIn">
            <button @click="logout" class="btn btn-light rounded-3">
              Logout
            </button>
          </template>
          <template v-else>
            <RouterLink :to="{ name: 'login' }" class="btn btn-light rounded-3"
              >Login</RouterLink
            >
          </template>
        </div>
      </div>
    </nav>
  </header>
</template>
