<template>
    <div class="logo-container">
        <img class="logo" src="../assets/resturant-logo.jpg" />
    </div>
    <h1 class=" mt-8 mb-12 text-3xl font-bold text-fuchsia-900 ">
        Login
    </h1>
    <div class="login">
        <!-- <input type="text" v-model="email" placeholder="Enter Email" /> -->
        <div class="mb-6">
            <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Email
                address</label>
            <input type="email" v-model="email" id="email"
                class="bg-gray-50 border text-fuchsia-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="john.doe@company.com" required />
        </div>
        <!-- <input type="password" v-model="password" placeholder="Enter Password" /> -->
        <div class="mb-6">
            <label for="password"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-fuchsia-900">Password</label>
            <input type="password" v-model="password" id="password"
                class="bg-gray-50 border border-gray-300 text-fuchsia-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 "
                placeholder="•••••••••" required />
        </div>
        <!-- <button v-on:click="login">Login</button> -->
        <div class="mb-6">
            <button type="button" v-on:click="login"
                class="text-white bg-fuchsia-950 hover:bg-fuchsia-800 focus:ring-1 focus:outline-none focus:ring-purple-800 dark:focus:ring-purple-800 font-medium rounded-lg text-xs px-3 py-1.5 text-center me-2 mb-2"
                style="width: 300px;">Login</button>

        </div>
        <p>
            <router-link class="underline text-fuchsia-900" to="/sign-up">Sign Up</router-link>
        </p>
    </div>
</template>
<script>
import axios from 'axios';
export default
    {
        name: "LoginPage",
        data() {
            return {
                email: '',
                password: ''
            }
        },
        methods: {
            async login() {
                let result = await axios.get(
                    `http://localhost:3000/users?email=${this.email}&password=${this.password}`
                )
                if (result.status == 200 && result.data.length > 0) {
                    localStorage.setItem("user-info", JSON.stringify(result.data[0]))
                    this.$router.push({ name: "HomePage" })
                }
                console.log(result);

            }
        },
        mounted() {
            let user = localStorage.getItem('user-info');
            if (user) {
                this.$router.push({ name: 'HomePage' })
            }
        }
    }
</script>
<style>
.logo-container {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
}

.logo {
    width: 100px;
}
</style>