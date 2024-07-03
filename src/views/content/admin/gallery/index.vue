<!-- @format -->

<template>
  <AdminLayout>

    <HeaderDashboard title="Galleries" pretitle="GALLERIES">
      <button type="button" class="btn btn-outline-secondary">+ Add Gallery</button>
    </HeaderDashboard>

    <div class="col-lg-12" v-if="dataGalleries.length === 0">
        <div class="card col-12">
            <div class="card-body">
                <h5 class="card-title text-center">Loading...</h5>
            </div>
        </div>
    </div>

    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 row-cols-xl-4 g-4">
      <div class="col" v-for="(data, index) in dataGalleries" :key="index">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title fs-6">{{ data.name }}</h5>
            <p class="card-text" v-if="data.description.length < 40">
              {{ data.description }}
            </p>
            <p class="card-text" v-else>
                {{ data.description.substring(0, 40) }}...
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

const dataGalleries = ref([]);

const fetchGalleries = async () => {
    await Api.get('/galleries')
    .then(response => {
        dataGalleries.value = response.data.data;
    })
    .catch(error => {
        console.log(error);
    })
}

onMounted(() => {
    fetchGalleries();
})

</script>
