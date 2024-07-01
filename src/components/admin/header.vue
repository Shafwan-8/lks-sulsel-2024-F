<template>
  <div class="row align-items-center mb-2 d-print-none mt-4">
            <div class="col text-dark">
            <div class="page-pretitle">
                {{ pretitle }}
            </div>

            <h4 class="page-title">
                {{ title }}
            </h4>
        </div>

    <div class="col-auto ms-auto d-print-none ">
        <div class="btn-list">
            <button type="button" class="btn btn-primary mx-3" onclick="window.print()">Cetak</button>
            <a href="#" class="btn d-none d-sm-inline-block btn-outline-secondary">Kembali</a>
        </div>
    </div>
</div>
</template>

<script setup>
defineProps(['title', 'pretitle'])
</script>