<template>
  <AdminLayout>
    <HeaderDashboard title="Dashboard" pretitle="DASHBOARD" />


  </AdminLayout>
</template>

<script setup>
import Cookies from 'js-cookie'
import { ref } from 'vue'
import { useRouter, RouterLink } from 'vue-router'
import Api from '../../../api'
import HeaderDashboard from '@/components/admin/headerDashboard.vue'
import AdminLayout from '../../../layouts/admin/MainLayout.vue'

const isLoggedIn = ref(false);
const router = useRouter();

const logout = async () => {
    try {
        // Get the token from cookies
        const token = Cookies.get('token');
        
        // Send a request to the backend to delete the token
        await Api.post('/logout', {}, {
            headers: {
                'Authorization': `Bearer ${token}`
            }
        });
    } catch (error) {
        console.error('Failed to logout from backend:', error);
    }
    
    // Remove the token from cookies
    Cookies.remove('token');
    isLoggedIn.value = false;
    router.push({ name: 'login' });
};

const alertse = () => {
  alert('New event')
}
</script>

