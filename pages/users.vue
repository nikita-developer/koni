<template>
    <div class="login">
        <button @click="getUsers">Получить список пользователей</button>
        <ul v-for="user in users" :key="user.id">
            <li>Id: {{user._id}}</li>
            <li>Имя: {{user.name}}</li>
            <li>Почта: {{user.email}}</li>
            <li>Пароль: {{user.password}}</li>
        </ul>
    </div>
</template>

<script setup>
import {ref} from "vue";

    const users = ref('')

    const getUsers = async () => {
        const settings = {
            method: 'GET',
            headers: {
                Accept: 'application/json',
                'Content-Type': 'application/json',
                Authorization: localStorage.getItem('token')
            },
        }
        try {
            const fetchResponse = await fetch('http://localhost:5000/api/users', settings)
            const data = await fetchResponse.json();
            users.value = data
        } catch (e) {
            return e
        }
    }
</script>

<style scoped lang="scss">
.login {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-grow: 1;
}

.login-form {
    padding: 30px 15px;

    &__label {
        display: block;
        margin-bottom: 15px;
    }
}
</style>
