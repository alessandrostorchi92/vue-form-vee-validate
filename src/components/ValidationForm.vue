<script>

export default {

    data() {

        return {

            form: {
                email: "",
                password: ""
            },

        };

    }

}

</script>


<template>

<form>

    <label for="email">Email</label>
    <input id="email" type="email" v-model="form.email">

    <label for="password">Password</label>
    <input id="password" type="password" v-model="form.password">

    <button>Submit</button>

</form>


</template>


<style lang="scss" scoped>


</style>