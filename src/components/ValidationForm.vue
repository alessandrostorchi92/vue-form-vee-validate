<script>

export default {

    data() {

        return {

            form: {

                name: "",
                surname: "",
                email: "",
                password: ""

            },

        };

    }

}

</script>


<template>

    <form>

        <label for="name">Name</label>
        <input id="name" type="text" name="name" v-model="form.name">

        <label for="surnmame">Surname</label>
        <input id="surname" type="text" name="surname" v-model="form.surname">

        <label for="email">Email</label>
        <input id="email" type="email" name="email" v-model="form.email">

        <label for="password">Password</label>
        <input id="password" type="password" name="password" v-model="form.password">

        <button>Submit</button>

    </form>


</template>


<style lang="scss" scoped></style>