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

        <div class="container">

            <div class="row justify-content-center mt-5">

                <div class="mb-3">

                    <label for="name" class="form-label">Name</label>
                    <input id="name" class="form-control" type="text" name="name" placeholder="Enter your name"
                        v-model="form.name">

                </div>

                <div class="mb-3">

                    <label for="surnmame" class="form-label">Surname</label>
                    <input id="surname" class="form-control" type="text" name="surname" placeholder="Enter your surname"
                        v-model="form.surname">

                </div>

                <div class="mb-3">

                    <label for="email" class="form-label">Email</label>
                    <input id="email" class="form-control" type="email" name="email" placeholder="Enter your email"
                        v-model="form.email">

                </div>

                <div class="mb-3">

                    <label for="password" class="form-label">Password</label>
                    <input id="password" class="form-control" type="password" name="password"
                        placeholder="Enter your password" v-model="form.password">

                </div>

                <div class="text-center">
                    <button type="submit" class="btn btn-primary">Submit</button>
                </div>

            </div>

        </div>

    </form>


</template>


<style lang="scss" scoped></style>