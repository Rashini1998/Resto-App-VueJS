<template>
    <PageHeader/>
    <h1>Hello {{name}}, Welcome to the Home Page!</h1>
    <table border="1px">
        <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Contact</th>
            <th>Address</th>
        </tr>
        <tr v-for="item in restuarant" :key="item.id">
            <td>
                {{ item.id }}
            </td>
            <td>
                {{ item.name }}
            </td>
            <td>
                {{ item.contact }}
            </td>
            <td>
                {{ item.address }}
            </td>
        </tr>
    </table>
</template>
<script>
import PageHeader from './Header.vue';
import axios from 'axios';
    export default
    {
        name:"HomePage",
        components:{
            PageHeader
        },
        data()
        {
            return{
                name:'',
                restuarant:[],
            }
        },
        async mounted()
        {
        let user = localStorage.getItem('user-info');
        this.name=JSON.parse(user).name;
            if(!user)
            {
                this.$router.push({name:'SignUp'}) 
            }
            let result = await axios.get("http://localhost:3000/restuarant");
            this.restuarant=result.data;
        }
    }
</script>
<style>
    td{
        width:160px;
        height: 40px;

    }
</style>