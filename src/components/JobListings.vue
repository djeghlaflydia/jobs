<script setup>
import JobListing from "@/components/JobListing.vue";
import JobData from "@/jobs copy.json";
import {ref} from 'vue';

const jobs = ref(JobData);
//console.log(jobs.value);

</script>

<template>

    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl front-bold text-green-500 mb-6 text-center">
                Brrows jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in jobs" :key="job.id"    :job="job"/>
            </div>

        </div>
    </section>

    

</template>