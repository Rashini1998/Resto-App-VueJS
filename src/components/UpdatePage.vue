<template>
    <PageHeader/>
    <!-- <h1>Hello User, Welcome to the Update Restuarant Page!</h1> -->
    <h1 class=" mt-8 mb-12 text-3xl font-bold ">
        Hello User, Welcome to the Update Restuarant Page!
  </h1>
</template>
<script>
import PageHeader from './Header.vue';
    export default
    {
        name:"UptadePage",
        components:{
            PageHeader
        },
        mounted()
        {
        let user = localStorage.getItem('user-info');
            if(!user)
            {
                this.$router.push({name:'SignUp'}) 
            }
        }
    }
</script>
<style></style>