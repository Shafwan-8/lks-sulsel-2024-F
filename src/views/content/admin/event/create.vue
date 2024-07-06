<!-- @format -->

<template>
    <AdminLayout>
      <HeaderDashboard title="Event Create" pretitle="EVENT">
        <RouterLink :to="{name: 'admin-event'}" class="btn btn-outline-secondary">Back</RouterLink>
      </HeaderDashboard>
  
      <form @submit.prevent="store">
        <div class="col-md-6">
          <div class="form-group mb-3">
            <label for="name">Name</label>
            <input
              type="text"
              class="form-control"
              id="name"
              name="name"
              v-model="name"
            />
            <div v-if="errors.name" class="alert alert-danger mt-2">
              <span>{{ errors.name[0] }}</span>
            </div>
          </div>
          <div class="form-group mb-3">
            <label for="description">Description</label>
            <textarea
              class="form-control"
              id="description"
              name="description"
              v-model="description"
              rows=""
            ></textarea>
            <div v-if="errors.description" class="alert alert-danger mt-2">
              <span>{{ errors.description[0] }}</span>
            </div>
          </div>
          <div class="form-group mb-3">
            <label for="date_start">Start Date</label>
            <input type="date" class="form-control" id="date_start" name="date_start" v-model="date_start" />
          </div>
          <div class="form-group mb-3">
            <label for="date_end">End Date</label>
            <input type="date" class="form-control" id="date_end" name="date_end" v-model="date_end" />
          </div>
          <div class="form-group mb-3">
            <label for="price">Price</label>
            <input
              type="number"
              class="form-control"
              id="price"
              name="price"
              v-model="price"
            />
            <div v-if="errors.price" class="alert alert-danger mt-2">
              <span>{{ errors.price[0] }}</span>
            </div>
          </div>
          <button type="submit" class="btn btn-primary">Save</button>
        </div>
      </form>
    </AdminLayout>
  </template>
  
  <script setup>
  import AdminLayout from "@/layouts/admin/MainLayout.vue";
  import HeaderDashboard from "@/components/admin/headerDashboard.vue";
  import { ref, onMounted } from "vue";
  import { useRouter, RouterLink } from "vue-router";
  import cookie from "js-cookie";
  import Api from "@/api";
  
  const router = useRouter();
  
  const name = ref("");
  const description = ref("");
  const date_start = ref("");
  const date_end = ref("");
  const price = ref("");
  const errors = ref([]);
  
  const token = cookie.get("token");
  
  const store = async () => {
    let formData = new FormData();
  
    formData.append("name", name.value);
    formData.append("description", description.value);
    formData.append("date_start", date_start.value);
    formData.append("date_end", date_end.value);
    formData.append("price", price.value);
  
    await Api.post("/admin/event/create", formData, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    })
      .then(() => {
        router.push({ name: "admin-event" });
      })
      .catch((error) => {
        console.error("Error response:", error.response.data); // Log error response
        errors.value = error.response.data;
      });
  };
  </script>
  