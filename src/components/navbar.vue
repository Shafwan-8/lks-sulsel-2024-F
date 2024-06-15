<script setup>
import { RouterLink, RouterView } from 'vue-router'


</script>

<template lang="">
  <header>
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark mb-5">
      <div class="container-lg">
        <a class="navbar-brand" href="#">Carousel</a>
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
                <li><RouterLink class="dropdown-item" :to="{name: 'destinations'}">Destinations</RouterLink></li>
                <li><RouterLink class="dropdown-item" :to="{name: 'events'}">Events</RouterLink></li>
                <li><RouterLink class="dropdown-item" :to="{name: 'posts'}">Posts</RouterLink></li>
                <li><RouterLink class="dropdown-item" :to="{name: 'galleries'}">Galleries</RouterLink></li>
              </ul>
            </li>
          </ul>
          <div class="me-auto"></div>
          <RouterLink :to="{ name: 'login' }" class="btn btn-light rounded-3">Login</RouterLink>
        </div>
      </div>
    </nav>
  </header>
</template>
