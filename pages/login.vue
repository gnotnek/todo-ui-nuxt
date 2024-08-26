<template>
    <div>
        <h1>Login</h1>
        <form @submit="handleLogin">
            <label for="email">Email:</label>
            <input type="email" id="email" v-model="email" required>
            
            <label for="password">Password:</label>
            <input type="password" id="password" v-model="password" required>
            
            <button type="submit">Login</button>
        </form>
        <router-link to="/">Back</router-link>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const router = useRouter()

const handleLogin = async (event) => {
    event.preventDefault()
    const response = await fetch('http://localhost:3500/login', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            email: email.value,
            password: password.value
        })
    })
    const data = await response.json()
    if (data.error) {
        alert(data.error)
        return
    }
    console.log(data)
    router.push('/')
}
</script>