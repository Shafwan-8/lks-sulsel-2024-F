<!-- @format -->

<template>
  <AdminLayout>
    <HeaderDashboard title="Post Edit" pretitle="POST">
      <RouterLink
        :to="{ name: 'admin-post' }"
        class="btn btn-outline-secondary"
        >Back</RouterLink
      >
    </HeaderDashboard>

    <form @submit.prevent="store">
      <div class="col-md-6">
        <div class="form-group mb-3">
          <label for="title">Title</label>
          <input
            type="text"
            class="form-control"
            id="title"
            name="title"
            v-model="title"
          />
          <div v-if="errors.title" class="alert alert-danger mt-2">
            <span>{{ errors.title[0] }}</span>
          </div>
        </div>
        <div class="form-group mb-3">
          <label for="category_id">Category</label>
          <select
            class="form-select"
            id="category_id"
            name="category_id"
            v-model="category_id"
          >
            <option
              v-for="category in categories"
              :key="category.id"
              :value="category.id"
            >
              {{ category.name }}
            </option>
          </select>
          <div v-if="errors.category_id" class="alert alert-danger mt-2">
            <span>{{ errors.category_id[0] }}</span>
          </div>
        </div>
        <div class="form-group mb-3">
          <label for="content">Content</label>
          <textarea
            class="form-control"
            id="content"
            name="content"
            v-model="content"
            rows="3"
          ></textarea>
          <div v-if="errors.content" class="alert alert-danger mt-2">
            <span>{{ errors.content[0] }}</span>
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
import { useRouter, useRoute, RouterLink } from "vue-router";
import cookie from "js-cookie";
import Api from "@/api";

const router = useRouter();
const route = useRoute();

const title = ref("");
const categories = ref([]);
const category_id = ref("");
const content = ref("");
const errors = ref([]);

const token = cookie.get("token");

const store = async () => {
  let formData = new FormData();

  formData.append("title", title.value);
  formData.append("category_id", category_id.value);
  formData.append("content", content.value);

  await Api.put(`/admin/post/${route.params.id}`, formData, {
    headers: {
      Authorization: `Bearer ${token}`,
    },
  })
    .then(() => {
      router.push({ name: "admin-post" });
    })
    .catch((error) => {
      console.error("Error response:", error.response.data); // Log error response
      errors.value = error.response.data;
    });
};

const getPost = async () => {
  try {
    const response = await Api.get(`/admin/post/${route.params.id}}`);

    title.value = response.data.data.title;
    category_id.value = response.data.data.category_id;
    content.value = response.data.data.content;
  } catch {
    console.error("Error response:", error.response.data); // Log error response
    errors.value = error.response.data;
  }
};

const fetchCategories = async () => {
  await Api.get("/admin/category")
    .then((response) => {
      categories.value = response.data.data;
    })
    .catch((error) => {
      console.error("Error response:", error.response.data); // Log error response
      errors.value = error.response.data;
    });
};

onMounted(() => {
  fetchCategories();
  getPost();
});
</script>
