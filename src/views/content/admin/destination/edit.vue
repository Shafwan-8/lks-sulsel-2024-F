<template>
  <AdminLayout>
    <HeaderDashboard title="Destinations Edit" pretitle="DESTINATIONS">
      <RouterLink :to="{name: 'admin-destination'}" class="btn btn-outline-secondary">Back</RouterLink>
    </HeaderDashboard>

    <form @submit.prevent="edit">
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
            rows="10"
          >
          {{ description }}
        </textarea>
          <div v-if="errors.description" class="alert alert-danger mt-2">
            <span>{{ errors.description[0] }}</span>
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
import { useRoute, useRouter } from "vue-router";
import cookie from "js-cookie";
import Api from "@/api";

const router = useRouter();
const route = useRoute()

const name = ref();
const description = ref();
const errors = ref([]);

const token = cookie.get("token");

const fetchDestinasi = async () => {

    await Api.get(`/admin/destination/${route.params.id}`, {
        headers: {
            Authorization: `Bearer ${token}`,
        }
    })
    .then((response) => {
        name.value = response.data.data.name;
        description.value = response.data.data.description;
    })
    .catch(error => {
        console.log(error);
    })
}

onMounted(() => {
    fetchDestinasi();
})

const edit = async () => {
  let formData = new FormData();

  formData.append("name", name.value);
  formData.append("description", description.value);

  await Api.put(`/admin/destination/${route.params.id}`, formData, {
    headers: {
      Authorization: `Bearer ${token}`,
    },
  })
    .then(() => {
      router.push({ name: "admin-destination" });
    })
    .catch((error) => {
      console.error("Error response:", error.response.data); // Log error response
      errors.value = error.response.data;
    });
};
</script>
