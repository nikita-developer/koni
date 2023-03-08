<template>
    <div class="registration">
        <form @submit.prevent="submit" class="registration-form">
            <h2 class="registration-form__title">Регистрация</h2>
            <label class="registration-form__label">
                <p class="registration-form__placeholder">Введите ваш логин</p>
                <input v-model="email" type="text" class="registration-form__field">
            </label>
            <label class="registration-form__label">
                <p class="registration-form__placeholder">Введите вашe имя</p>
                <input v-model="name" type="text" class="registration-form__field">
            </label>
            <label class="registration-form__label">
                <p class="registration-form__placeholder">Придумайте пароль</p>
                <input v-model="password" type="text" class="registration-form__field">
            </label>
            <button class="registration-form__btn">Зарегистрироваться</button>
            <div class="registration-form__footer">
                <NuxtLink to="/login">Войти</NuxtLink>
            </div>
        </form>
    </div>
</template>

<script setup>
    import {ref} from 'vue'

    const email = ref('')
    const name = ref('')
    const password = ref('')

    const submit = async () => {
        const settings = {
            method: 'POST',
            headers: {
                Accept: 'application/json',
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                email: email.value,
                name: name.value,
                password: password.value,
            })
        }
        try {
            const fetchResponse = await fetch('http://localhost:5000/api/auth/registration', settings)
            const data = await fetchResponse.json();
            return console.log(data)
        } catch (e) {
            return e
        }
    }
</script>

<style scoped lang="scss">
.registration {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-grow: 1;
}

.registration-form {
    padding: 30px 15px;

    &__label {
        display: block;
        margin-bottom: 15px;
    }
}
</style>
