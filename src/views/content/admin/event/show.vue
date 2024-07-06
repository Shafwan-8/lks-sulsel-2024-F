<template>
    <AdminLayout>
        <HeaderDashboard title="Event Show" pretitle="EVENT">
            <RouterLink :to="{name: 'admin-event'}" class="btn btn-outline-secondary">
                Back
            </RouterLink>
            <RouterLink :to="{name: 'admin-event-edit', params: {id: $route.params.id}}" class="btn btn-warning ms-3 text-white">
                Edit
            </RouterLink>
        </HeaderDashboard>
    
        <div class="col-12" v-if="dataEvent.length === 0">
            <div class="card">
                <div class="card-body text-center">
                  Loading...  
                </div>
            </div>
        </div>
    
    
        <div class="col-6" v-else>
            <div class="mb-2">
                <h2 class="mb-0">{{ dataEvent.name }}</h2>
                <span class="lead" style="font-size: medium;">By: {{ dataEvent.user }}</span>
            </div>

            <p class="mt-3">{{ dataEvent.description }}</p>

            <div class="mb-3 d-flex flex-column">
                <span class="fw-light">Start Date : {{ dataEvent.date_start }}</span>
                <span class="fw-light">End Date: {{ dataEvent.date_end }}</span>
                <span class="fw-light">Price: <u>${{ dataEvent.price }}</u></span>
            </div>
            
        </div>
    </AdminLayout>
    </template>
    
    <script setup>
    import AdminLayout from "@/layouts/admin/MainLayout.vue";
    import HeaderDashboard from "@/components/admin/headerDashboard.vue";
    import { useRoute, useRouter, RouterLink } from "vue-router";
    import {ref, onMounted} from 'vue'
    import Cookie from 'js-cookie'
    import Api from '@/api'
    
    const token = Cookie.get('token');
    const dataEvent = ref("")
    const route = useRoute()

    const fetchData = async () => {
    
        try
        {
            const response = await Api.get(`/admin/event/${route.params.id}`, {
                headers: {
                    'Authorization': `Bearer ${token}`
                }
            })
            dataEvent.value = response.data.data
            console.log(response.data.data)
            
        }
        catch (error)
        {
            console.log(error)
        }
    
    
    }
    
    onMounted(() => {
        fetchData()
    })
    
    </script>