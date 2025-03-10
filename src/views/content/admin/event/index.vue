<!-- @format -->

<template>
  <AdminLayout>
    <HeaderDashboard title="Events" pretitle="EVENTS">
      <RouterLink :to="{name: 'admin-event-create'}" class="btn btn-outline-secondary">
        + Add Event
      </RouterLink>
    </HeaderDashboard>

    <div class="col-lg-12" v-if="deleteStatus">
      <div class="alert alert-success alert-dismissible fade show" role="alert">
        Success Deleted Data!
        <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
      </div>
    </div>

    <div class="col-lg-12" v-if="dataEvents.length === 0">
      <div class="card col-12">
        <div class="card-body">
          <h5 class="card-title text-center">Loading...</h5>
        </div>
      </div>
    </div>

    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 row-cols-xl-4 g-4">
      <div class="col" v-for="(data, index) in dataEvents" :key="index">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ data.name }}</h5>
            <p class="card-text" v-if="data.description.length < 40">
              {{ data.description }}
            </p>
            <p class="card-text" v-else>
              {{ data.description.substring(0, 40) }}...
            </p>
          </div>
          <div class="card-footer d-flex justify-content-end">
            <span class="lead" style="font-size: 1rem"
              >By: {{ data.user }}</span
            >
            <router-link :to="{name: 'admin-event-show', params: {id: data.id}}" class="btn btn-primary btn-sm ms-auto">View</router-link>
            <button @click="destroy(data.id)" class="btn btn-danger btn-sm ms-2">Delete</button>
          </div>
        </div>
      </div>
    </div>

    <div class="alert alert-danger" v-if="errorMessage">
      {{ errorMessage }}
    </div>

  </AdminLayout>
</template>

<script setup>
import AdminLayout from "@/layouts/admin/MainLayout.vue";
import HeaderDashboard from "@/components/admin/headerDashboard.vue";
import { ref, onMounted } from "vue";
import { RouterLink } from "vue-router";
import Cookie from "js-cookie";
import Api from "@/api";

const token = Cookie.get("token");
const dataEvents = ref([]);
const errorMessage = ref('');

let deleteStatus = false;

const fetchEvents = async () => {
  try {
    const response = await Api.get("/admin/event", {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    dataEvents.value = response.data.data;
  } catch (error) {
    console.log(error);
    errorMessage.value = error.response
      ? error.response.data.message
      : error.message; // Store error message
  }
};

const destroy = async (id) => {

  let confirmm = confirm('Are you sure you want to delete this event?')

  if (confirmm)
  {
    await Api.delete(`/admin/event/${id}`)
    .then(() => {
      fetchEvents();
      deleteStatus = true;
    })
    .catch((error) => {
      console.log(error);
    })

  }
}

onMounted(() => {
  fetchEvents();
});
</script>
