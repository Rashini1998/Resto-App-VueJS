<template>
    <PageHeader />
    <!-- <h1>Hello User, Welcome to the Add Restuarant Page!</h1> -->
    <h1 class=" mt-8 mb-12 text-3xl font-bold ">
        Hello User, Welcome to the Add Restuarant Page!
    </h1>
    <div class="addResto">
        <div class="mb-6">
            <label for="text" class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Name</label>
            <input type="text" v-model="restuarant.name" id="name" name="name"
                class="bg-gray-50 border text-fuchsia-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="Enter Name" required />
        </div>
        <div class="mb-6">
            <label for="text" class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Address</label>
            <input type="email" v-model="restuarant.address" id="address" name="address"
                class="bg-gray-50 border text-fuchsia-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="Enter Address" required />
        </div>
        <div class="mb-6">
            <label for="text" class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Contact</label>
            <input type="password" v-model="restuarant.contact" id="contact"
                class="bg-gray-50 border border-gray-300 text-fuchsia-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="Enter Contact Number" required />
        </div>
        <div class="mb-6">
            <button type="button" v-on:click="addResto"
                class="text-white bg-fuchsia-950 hover:bg-fuchsia-800 focus:ring-1 focus:outline-none focus:ring-purple-800 dark:focus:ring-purple-800 font-medium rounded-lg text-xs px-3 py-1.5 text-center me-2 mb-2"
                style="width: 300px;">Add New Restuarant</button>

        </div>

    </div>
</template>
<script>
import PageHeader from './Header.vue';
export default
    {
        name: "AddPage",
        components: {
            PageHeader
        },
        data() {
            return {
                restuarant: {
                    name: '',
                    address: '',
                    contact: ''
                }
            }

        },
        methods:{
            addResto(){
                console.log(this.restuarant);
                
            }
        },
        mounted() {
            let user = localStorage.getItem('user-info');
            if (!user) {
                this.$router.push({ name: 'SignUp' })
            }
        }
    }
</script>
<style></style>