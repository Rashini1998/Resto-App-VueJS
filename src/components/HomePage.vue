<template>
    <PageHeader />
    <h1 class="mt-8 mb-12 text-3xl font-bold">
        Hello {{ name }}, Welcome to the Home Page!
    </h1>

    <div class="relative overflow-x-auto px-8">
        <table class="w-full text-sm text-center rtl:text-right text-gray-500">
            <thead class="text-s text-fuchsia-950 uppercase bg-gray-50">
                <tr>
                    <!-- <th scope="col" class="column-header">
                        ID
                    </th> -->
                    <th scope="col" class="column-header">
                        Name
                    </th>
                    <th scope="col" class="column-header">
                        Contact
                    </th>
                    <th scope="col" class="column-header">
                        Address
                    </th>
                    <th scope="col" class="column-header">
                        Actions
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr class="bg-white border-b" v-for="item in restuarant" :key="item.id">
                    <!-- <th scope="row" class="column-cell font-medium text-gray-900 text-slate-800">
                        {{ item.id }}
                    </th> -->
                    <td class="column-cell">
                        {{ item.name }}
                    </td>
                    <td class="column-cell">
                        {{ item.contact }}
                    </td>
                    <td class="column-cell">
                        {{ item.address }}
                    </td>
                    <td class="column-cell">
                        <router-link :to="'/update/' + item.id" class="btn btn-green">Update</router-link>
                        <button v-on:click="deleteResto(item.id)" class="btn btn-red">Delete </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import PageHeader from './Header.vue';
import axios from 'axios';
import Swal from 'sweetalert2';

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
    methods: {
        // async deleteResto(id) {
        //     let result = await axios.delete("http://localhost:3000/restuarant/" + id);
        //     console.warn(result.status);
        //     if (result.status == 200) {
        //         this.loadData();
        //     }
        // },
        async deleteResto(id) {
            Swal.fire({
                title: "Are you sure?",
                text: "You won't be able to revert this!",
                icon: "warning",
                showCancelButton: true,
                confirmButtonColor: "#3085d6",
                cancelButtonColor: "#d33",
                confirmButtonText: "Yes, delete it!"
            }).then(async (result) => {
                if (result.isConfirmed) {
                    try {
                        let response = await axios.delete("http://localhost:3000/restuarant/" + id);
                        if (response.status == 200) {
                            Swal.fire(
                                "Deleted!",
                                "Your file has been deleted.",
                                "success"
                            );
                            this.loadData();  // Reload the data after deletion
                        }
                    } catch (error) {
                        Swal.fire(
                            "Error!",
                            "There was an issue deleting the item.",
                            "error"
                        );
                        console.error("Error deleting restaurant:", error);
                    }
                }
            });
        },
        async loadData() {
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
    },
    async mounted() {
        this.loadData();
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

.btn {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    width: 90px;
    height: 35px;
    font-size: 14px;
    font-weight: 600;
    border-radius: 20px;
    cursor: pointer;
    text-decoration: none;
    transition: all 0.3s ease;
    margin-bottom: 8px;
    margin-top: 8px;

}

.btn-green {
    background-color: #16a34a;
    color: white;
    border: 1px solid #16a34a;
    margin-right: 16px;
}

.btn-red {
    background-color: #e11d48;
    color: white;
    border: 1px solid #e11d48;
}

/* Hover Effects */
.btn-green:hover {
    background-color: #15803d;
    border-color: #15803d;
    transform: scale(1.05);
}

.btn-red:hover {
    background-color: #be123c;
    border-color: #be123c;
    transform: scale(1.05);
}
</style>
