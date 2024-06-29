<template>
    <div class="d-flex justify-content-center align-items-center" style="height: 100vh">
        <div class="card" style="width: 25rem">
            <div class="card-body">
                <div class="py-3">
                    <h3 class="text-center">Login</h3>
                </div>
                <form @submit.prevent="login">
                    <div class="form-floating mb-3">
                        <input type="text" v-model="email" class="form-control" placeholder="Email">
                        <label for="email" class="text-muted">Email</label>
                    </div>
                    <div class="form-floating mb-3">
                        <input type="password" v-model="password" class="form-control" placeholder="password">
                        <label for="password" class="text-muted">Password</label>
                    </div>
                    <button class="btn btn-primary w-100 rounded-2">Login</button>
                </form>
            </div>
        </div>
    </div>

</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import Api from '../../api';
import Cookies from 'js-cookie';

const email = ref('');
const password = ref('');
const router = useRouter();

const login = async () => {
    try {
        const response = await Api.post('/login', { 
            email: email.value, 
            password: password.value 
        });
        if (response.data.status) {
            Cookies.set('token', response.data.token, { expires: 7 });
            router.push({ name: 'admin' });
        } else {
            alert('Login failed');
        }
    } catch (error) {
        console.error(error);
        alert('An error occurred');
    }
};
</script>
<style lang="">
    
</style>