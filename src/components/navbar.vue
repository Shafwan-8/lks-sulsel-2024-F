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
                <li><a class="dropdown-item" href="#">Destination</a></li>
                <li><a class="dropdown-item" href="#">Event</a></li>
                <li><a class="dropdown-item" href="#">Post</a></li>
                <li><a class="dropdown-item" href="#">Gallery</a></li>
              </ul>
            </li>
          </ul>
          <div class="me-auto"></div>
          <RouterLink :to="{ name: 'login' }" class="btn btn-light rounded-3">Masuk</RouterLink>
        </div>
      </div>
    </nav>
  </header>
</template>
