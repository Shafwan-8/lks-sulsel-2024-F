<template>
<AdminLayout>
    <HeaderDashboard title="Show" pretitle="DESTINATION">
        <RouterLink :to="{name: 'admin-destination'}" class="btn btn-outline-secondary">
            Back
        </RouterLink>
        <RouterLink :to="{name: 'admin-destination-edit', params: {id: $route.params.id}}" class="btn btn-warning ms-3 text-white">
            Edit
        </RouterLink>
    </HeaderDashboard>

    <div class="col-12" v-if="dataDestinasi.length === 0">
        <div class="card">
            <div class="card-body text-center">
              Loading...  
            </div>
        </div>
    </div>


    <div class="col-6">
        <h2>{{ dataDestinasi.name }}</h2>
        <p class="mt-3">{{ dataDestinasi.description }}</p>
    </div>
</AdminLayout>
</template>

<script setup>
import AdminLayout from "@/layouts/admin/MainLayout.vue";
import HeaderDashboard from "@/components/admin/headerDashboard.vue";
import { useRoute, useRouter, RouterLink } from "vue-router";
import {ref, onMounted} from 'vue'
import Api from '@/api'

const dataDestinasi = ref("")
const route = useRoute()

const fetchData = async () => {

    await Api.get(`/admin/destination/${route.params.id}`)
        .then(response => {
            dataDestinasi.value = response.data.data
            console.log(response)
        })
        .catch(error => {
            console.log(error)
        })


}

onMounted(() => {
    fetchData()
})

</script>