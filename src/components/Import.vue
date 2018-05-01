<template>
</template>

<script>
 import axios from 'axios'
 export const HTTP = axios.create({
     baseURL: `http://localhost:4567/`
 }) 
 export default {
 }
</script>
