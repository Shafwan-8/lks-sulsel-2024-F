
<template>
  <AdminLayout>
    
    <HeaderDashboard title="Destinations" pretitle="DESTINATIONS">
      <button type="button" class="btn btn-outline-secondary" @click="$router.push({name: 'admin-destination-create'})">+ Add Destination</button>
    </HeaderDashboard>

    <div class="col-lg-12" v-if="dataDestinations.length === 0">
        <div class="card col-12">
            <div class="card-body">
                <h5 class="card-title text-center">Loading...</h5>
            </div>
        </div>
    </div>

    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 row-cols-xl-4 g-4">
      <div class="col" v-for="(data, index) in dataDestinations" :key="index">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ data.name }}</h5>
            <p class="card-text" v-if="data.description.length < 30">
              {{ data.description }}
            </p>
            <p class="card-text" v-else>
                {{ data.description.substring(0, 40) }}...
            </p>
          </div>
          <div class="card-footer d-flex justify-content-end">
            <RouterLink :to="{name: 'admin-destination-show', params: {id: data.id}}" class="btn btn-primary btn-sm" @click="console.log('View')">View</RouterLink>
            <button class="btn btn-danger btn-sm ms-2" @click="destroy(data.id)">Delete</button>
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

const dataDestinations = ref([]);

const fetchDestinasi = async () => {
    await Api.get('/destination')
    .then(response => {
        dataDestinations.value = response.data.data;
    })
    .catch(error => {
        console.log(error);
    })
}

const debug = (id) => {
  confirm("ID: " + id);
}

const destroy = async (id) => {

  let confirmm = confirm('Are you sure you want to delete this destination?');

  if (confirmm) {
    
    await Api.delete(`/admin/destination/${id}`)
    .then(() => {
      fetchDestinasi();
    })
    .catch(error => {
      console.log(error);
    })

  }


}

onMounted(() => {
    fetchDestinasi();
})

</script>
