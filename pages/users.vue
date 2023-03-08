<template>
    <div class="login">
        <button @click="getUsers">Получить список пользователей</button>
    </div>
</template>

<script setup>
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
            const fetchResponse = await fetch('http://localhost:5000/api/category', settings)
            const data = await fetchResponse.json();
            return console.log(data)
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
