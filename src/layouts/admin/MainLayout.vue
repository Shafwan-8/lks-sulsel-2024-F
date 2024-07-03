<template>
  <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0 shadow">
    <a class="navbar-brand col-md-3 col-lg-2 mr-0 px-3" href="#">WS</a>
    <button
      class="navbar-toggler position-absolute d-md-none collapsed"
      type="button"
      data-toggle="collapse"
      data-target="#sidebarMenu"
      aria-controls="sidebarMenu"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <input
      class="form-control form-control-dark w-100"
      type="text"
      placeholder="Search"
      aria-label="Search"
    />
    <ul class="navbar-nav px-3">
      <li class="nav-item text-nowrap">
        <button class="nav-link" @click="logout">Logout</button>
      </li>
    </ul>
  </nav>

  <div class="container-fluid">
    <div class="row">
      <!-- Sidebar -->
      <nav
        id="sidebarMenu"
        class="col-md-3 col-lg-2 d-md-block bg-light collapse sidebar position-relative"
      >
        <div class="position-sticky pt-3">
          <ul class="nav flex-column" id="menu">
            <li class="nav-item">
              <RouterLink :to="{name: 'admin'}" :class="getLinkClass('admin')" aria-current="page">
                Dashboard
              </RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink :to="{ name: 'admin-destination' }" :class="getLinkClass('admin-destination')">
                Destinations
              </RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink :to="{ name: 'admin-event' }" :class="getLinkClass('admin-event')">
                Events
              </RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink :to="{ name: 'admin-post' }" :class="getLinkClass('admin-post')">
                Posts
              </RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink :to="{ name: 'admin-gallery' }" :class="getLinkClass('admin-gallery')">
                Gallery
              </RouterLink>
            </li>
            <li class="nav-item border-bottom">
              <a href="#submenu2" data-bs-toggle="collapse" class="nav-link">
                Registrations...</a
              >
              <ul
                class="collapse nav flex-column ms-2"
                id="submenu2"
                data-bs-parent="#menu"
              >
                <li class="w-100">
                  <RouterLink :to="{ name: 'admin-event' }" :class=" getLinkClass('admin-event')">
                    Events
                  </RouterLink>
                </li>
              </ul>
            </li>
          </ul>

          <h6
            class="sidebar-heading d-flex justify-content-between align-items-center px-3 mt-4 mb-1 text-muted"
          >
            <span>Administrator</span>
            <a class="link-secondary" href="#" aria-label="Add a new report">
              <span data-feather="plus-circle"></span>
            </a>
          </h6>
          <ul class="nav flex-column mb-2">
            <li class="nav-item">
              <a class="nav-link" href="#">
                <span data-feather="file-text"></span>
                User Admin
              </a>
            </li>
          </ul>
        </div>
      </nav>
      <!-- EndSidebar -->

      <main class="col-md-9 ml-sm-auto col-lg-10 px-md-4">
        <!-- Content -->
        <slot></slot>
        <!-- End Content -->
      </main>
    </div>
  </div>
</template>

<script setup>
import Cookies from 'js-cookie'
import { ref, computed } from 'vue'
import { useRouter, RouterLink } from 'vue-router'
import Api from '../../api'

const isLoggedIn = ref(false);
const router = useRouter();

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

const getLinkClass = (routeName) => {

  if (router.name === routeName) {
    return {
      'active': true,
    };
  }

  return {
    'nav-link': true,
  };

};
</script>

<style scoped>
.bd-placeholder-img {
  font-size: 1.125rem;
  text-anchor: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

@media (min-width: 768px) {
  .bd-placeholder-img-lg {
    font-size: 3.5rem;
  }
}

.feather {
  width: 16px;
  height: 16px;
  vertical-align: text-bottom;
}

/* Sidebar*/

.sidebar {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  z-index: 100;
  /* Behind the navbar */
  padding: 0 0 0;
  /* Height of navbar */
  box-shadow: inset -1px 0 0 rgba(0, 0, 0, 0.1);
}

@media (max-width: 767.98px) {
  .sidebar {
    top: 5rem;
  }
}

.sidebar-sticky {
  position: relative;
  top: 0;
  height: calc(100vh - 48px);
  padding-top: 0.5rem;
  overflow-x: hidden;
  overflow-y: auto;
  /* Scrollable contents if viewport is shorter than content. */
}

.sidebar .nav-link {
  font-weight: 500;
  color: #333;
}

.sidebar .nav-link .feather {
  margin-right: 4px;
  color: #727272;
}

.sidebar .nav-link.router-link-active {
  color: #007bff;
}

.sidebar .nav-link:hover .feather,
.sidebar .nav-link.active .feather {
  color: inherit;
}

.sidebar-heading {
  font-size: 0.75rem;
  text-transform: uppercase;
}

/*Navbar*/
.navbar-brand {
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  font-size: 1rem;
  background-color: rgba(0, 0, 0, 0.25);
  box-shadow: inset -1px 0 0 rgba(0, 0, 0, 0.25);
}

.navbar .navbar-toggler {
  top: 0.25rem;
  right: 1rem;
}

.navbar .form-control {
  padding: 0.75rem 1rem;
  border-width: 0;
  border-radius: 0;
}

.form-control-dark {
  color: #fff;
  background-color: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.1);
}

.form-control-dark:focus {
  border-color: transparent;
  box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.25);
}
</style>
