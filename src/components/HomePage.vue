<template>
    <PageHeader/>
    <h1>Hello User, Welcome to the Home Page!</h1>
</template>
<script>
import PageHeader from './Header.vue';
    export default
    {
        name:"HomePage",
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