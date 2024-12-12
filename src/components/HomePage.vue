<template>
    <h1>Hello User, Welcome to the Home Page!</h1>
</template>
<script>
    export default
    {
        name:"HomePage",
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