<script>

import { Form, Field } from 'vee-validate';

export default {

    components: {
        Form,
        Field,
    },

    data() {

        return {

            form: {

                name: "",
                surname: "",
                email: "",
                password: ""

            },

        };

    },

    methods: {

        onSubmit(values) {
            console.log(values);
        },

        validateEmail(value) {

            // if the field is null, undefined, o ""
            if (!value) {
                return "This field is required";
            };

            const emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;

            // if the field is not a valid email
            if (!emailPattern.test(value)) {

                return "You entered an invalid email"

            };

            return true;

        },

    }

}

</script>


<template>

    <Form @submit="onSubmit">

        <div class="container">

            <div class="row justify-content-center mt-5">

                <div class="mb-3">

                    <label for="name" class="form-label">Name</label>
                    <Field id="name" class="form-control" type="text" name="name" placeholder="Enter your name"
                        v-model="form.name"></Field>

                </div>

                <div class="mb-3">

                    <label for="surname" class="form-label">Name</label>
                    <Field id="surname" class="form-control" type="text" name="surname" placeholder="Enter your surname"
                        v-model="form.surname"></Field>

                </div>

                <div class="mb-3">

                    <label for="email" class="form-label">Email</label>
                    <Field id="email" class="form-control" type="email" name="email" placeholder="Enter your email"
                        v-model="form.email" :rules="validateEmail"></Field>

                </div>

                <div class="mb-3">

                    <label for="password" class="form-label">Password</label>
                    <Field id="password" class="form-control" type="password" name="password"
                        placeholder="Enter your password" v-model="form.password"></Field>

                </div>

                <div class="text-center">
                    <button type="submit" class="btn btn-primary">Submit</button>
                </div>

            </div>

        </div>

    </Form>

</template>


<style lang="scss" scoped></style>