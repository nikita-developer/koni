<template>
    <div class="login">
        <form @submit.prevent="submit" class="login-form">
            <h2 class="login-form__title">Авторизация</h2>
            <label class="login-form__label">
                <p class="login-form__placeholder">Введите ваш логин</p>
                <input v-model="email" type="text" class="login-form__field">
            </label>
            <label class="login-form__label">
                <p class="login-form__placeholder">Введите ваш пароль</p>
                <input v-model="password" type="text" class="login-form__field">
            </label>
            <button class="login-form__btn">Войти</button>
            <div class="login-form__footer">
                <NuxtLink to="/registration">Зарегистрироваться</NuxtLink>
            </div>
        </form>
    </div>
</template>

<script setup>
    import {ref, unref} from 'vue'

    const email = ref('')
    const password = ref('')

    const submit = async () => {
        const settings = {
            method: 'POST',
            headers: {
                Accept: 'application/json',
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                email: unref(email),
                password: unref(password),
            })
        }
        try {
            const fetchResponse = await fetch('http://localhost:5000/api/auth/login', settings)
            const data = await fetchResponse.json();
            localStorage.setItem('token', data.token)
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
