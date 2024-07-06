<template>
    <AdminLayout>
        <HeaderDashboard title="Post Show" pretitle="POST">
            <RouterLink :to="{name: 'admin-post'}" class="btn btn-outline-secondary">
                Back
            </RouterLink>
            <RouterLink :to="{name: 'admin-post-edit', params: {id: $route.params.id}}" class="btn btn-warning ms-3 text-white">
                Edit
            </RouterLink>
        </HeaderDashboard>
    
        <div class="col-12" v-if="dataPost.length === 0">
            <div class="card">
                <div class="card-body text-center">
                  Loading...  
                </div>
            </div>
        </div>
    
    
        <div class="col-6" v-else>
            <div class="mb-2 d-flex flex-column">
                <h2 class="mb-0">{{ dataPost.title }}</h2>
                <span class="lead" style="font-size: medium;">By: {{ dataPost.user }}</span>
                <span class="lead" style="font-size: medium;">Category: {{ dataPost.category }}</span>
            </div>

            <p class="mt-3">{{ dataPost.content }}</p>

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
    const dataPost = ref("")
    const route = useRoute()

    const fetchData = async () => {
    
        try
        {
            const response = await Api.get(`/admin/post/${route.params.id}`, {
                headers: {
                    'Authorization': `Bearer ${token}`
                }
            })
            dataPost.value = response.data.data
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