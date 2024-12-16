<template>
    <PageHeader/>
    <h1 class="mt-8 mb-12 text-3xl font-bold">
        Hello {{ name }}, Welcome to the Home Page!
    </h1>

    <div class="relative overflow-x-auto px-8">
        <table class="w-full text-sm text-center rtl:text-right text-gray-500">
            <thead class="text-s text-fuchsia-950 uppercase bg-gray-50">
                <tr>
                    <th scope="col" class="column-header">
                        ID
                    </th>
                    <th scope="col" class="column-header">
                        Name
                    </th>
                    <th scope="col" class="column-header">
                        Contact
                    </th>
                    <th scope="col" class="column-header">
                        Address
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr class="bg-white border-b" v-for="item in restuarant" :key="item.id">
                    <th scope="row" class="column-cell font-medium text-gray-900 text-slate-800">
                        {{ item.id }}
                    </th>
                    <td class="column-cell">
                        {{ item.name }}
                    </td>
                    <td class="column-cell">
                        {{ item.contact }}
                    </td>
                    <td class="column-cell">
                        {{ item.address }}
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import PageHeader from './Header.vue';
import axios from 'axios';

export default {
    name: "HomePage",
    components: {
        PageHeader
    },
    data() {
        return {
            name: '',
            restuarant: [],
        };
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'SignUp' });
        } else {
            this.name = JSON.parse(user).name;
        }

        try {
            let result = await axios.get("http://localhost:3000/restuarant");
            this.restuarant = result.data;
        } catch (error) {
            console.error("Error fetching restaurant data:", error);
        }
    }
};
</script>

<style>
.column-header,
.column-cell {
    width: 160px;
    height: 40px;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis; 
}

.column-header {
    background-color: #f3f4f6; 
    font-weight: bold;
}
</style>
