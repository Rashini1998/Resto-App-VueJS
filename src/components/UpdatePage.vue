<template>
    <PageHeader/>
    <!-- <h1>Hello User, Welcome to the Update Restuarant Page!</h1> -->
    <h1 class=" mt-8 mb-12 text-3xl font-bold ">
        Hello User, Welcome to the Update Restuarant Page!
  </h1>
  <div class="addResto">
        <div class="mb-6">
            <label for="text" class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Name</label>
            <input type="text" v-model="restuarant.name" id="name" name="name"
                class="bg-gray-50 border text-fuchsia-700 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="Enter Name" required />
        </div>
        <div class="mb-6">
            <label for="text" class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Address</label>
            <input type="email" v-model="restuarant.address" id="address" name="address"
                class="bg-gray-50 border text-fuchsia-700 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="Enter Address" required />
        </div>
        <div class="mb-6">
            <label for="text" class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Contact</label>
            <input type="text" v-model="restuarant.contact" id="contact"
                class="bg-gray-50 border border-gray-300 text-fuchsia-700 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="Enter Contact Number" required />
        </div>
        <div class="mb-6">
            <button type="button" v-on:click="updateResto"
                class="text-white bg-fuchsia-950 hover:bg-fuchsia-800 focus:ring-1 focus:outline-none focus:ring-purple-800 dark:focus:ring-purple-800 font-medium rounded-lg text-xs px-3 py-1.5 text-center me-2 mb-2"
                style="width: 300px;">Update Restuarant</button>

        </div>

    </div>
</template>
<script>
import PageHeader from './Header.vue';
import axios from 'axios';
    export default
    {
        name:"UptadePage",
        components:{
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
            async updateResto(){
                const result = await axios.put("http://localhost:3000/restuarant/"+this.$route.params.id,{
                    name:this.restuarant.name,
                    address:this.restuarant.address,
                    contact:this.restuarant.contact
                });
                if(result.status==200)
                {
                    this.$router.push({name:'HomePage'})
                }
            }
        },
       async mounted()
        {
        let user = localStorage.getItem('user-info');
            if(!user)
            {
                this.$router.push({name:'SignUp'}) 
            }
            const result = await axios.get('http://localhost:3000/restuarant/'+this.$route.params.id);
            this.restuarant=result.data;
        }
    }
</script>
<style></style>
