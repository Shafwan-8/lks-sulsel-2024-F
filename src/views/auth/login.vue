<template>
    <div class="d-flex justify-content-center align-items-center" style="height: 100vh">
        <div class="card" style="width: 25rem">
            <div class="card-body">
                <div class="py-3">
                    <h3 class="text-center">Login</h3>
                </div>
                <form action="#">
                    <div class="form-floating mb-3">
                        <input type="text" name="email" id="email" class="form-control" placeholder="Email">
                        <label for="email" class="text-muted">Email</label>
                    </div>
                    <div class="form-floating mb-3">
                        <input type="text" name="password" id="password" class="form-control" placeholder="password">
                        <label for="password" class="text-muted">Password</label>
                    </div>
                    <button class="btn btn-primary w-100 rounded-2">Login</button>
                </form>
            </div>
        </div>
    </div>

</template>

<script setup>

</script>
<style lang="">
    
</style>