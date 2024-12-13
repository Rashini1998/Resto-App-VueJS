<template>
    <div class="nav">
        <a href="#">Home</a>
        <a href="#">Add Restaurant</a>
        <a href="#">Update Restaurant</a>
        <a href="#">Logout</a>
    </div>
</template>
<script>
export default {
    name: "PageHeader"
}
</script>
<style>
.nav{
    background-color: purple;
    overflow: hidden;
}
.nav a{
    float: left;
    color: aliceblue;
    padding: 14px 16px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
    background-color: rgb(222, 134, 222);
    color: purple;
}
</style>