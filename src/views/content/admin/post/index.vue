<!-- @format -->

<template>
  <AdminLayout>

    <HeaderDashboard title="Posts" pretitle="POSTS">
      <button type="button" class="btn btn-outline-secondary">+ Add Post</button>
    </HeaderDashboard>

    <div class="col-lg-12" v-if="dataPosts.length === 0">
        <div class="card col-12">
            <div class="card-body">
                <h5 class="card-title text-center">Loading...</h5>
            </div>
        </div>
    </div>

    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 row-cols-xl-4 g-4">
      <div class="col" v-for="(data, index) in dataPosts" :key="index">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title fs-6">{{ data.title }}</h5>
            <h6 class="card-subtitle text-muted mb-2" style="font-size: 0.8rem;">Category: {{ data.category }}</h6> 
            <p class="card-text" v-if="data.content.length < 40">
              {{ data.content }}
            </p>
            <p class="card-text" v-else>
                {{ data.content.substring(0, 40) }}...
            </p>
          </div>
          <div class="card-footer d-flex justify-content-end">
            <span class="lead" style="font-size: 0.8rem;">By: {{ data.user }}</span>
            <button class="btn btn-primary btn-sm ms-auto">View</button>
            <button class="btn btn-danger btn-sm ms-2">Delete</button>
          </div>
        </div>
      </div>
    </div>

  </AdminLayout>
</template>

<script setup>
import AdminLayout from "@/layouts/admin/MainLayout.vue";
import HeaderDashboard from "@/components/admin/headerDashboard.vue";
import { ref, onMounted } from "vue";
import Api from '@/api';

const dataPosts = ref([]);

const fetchPosts = async () => {
    await Api.get('/posts')
    .then(response => {
        dataPosts.value = response.data.data;
    })
    .catch(error => {
        console.log(error);
    })
}

onMounted(() => {
    fetchPosts();
})

</script>
