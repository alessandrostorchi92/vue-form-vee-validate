<script>

import { Form, Field, ErrorMessage, configure } from 'vee-validate';
import * as yup from 'yup';

configure({
    validateOnChange: true,
});

export default {

    components: {

        Form,
        Field,
        ErrorMessage

    },

    data() {

        return {

            form: {

                name: "",
                surname: "",
                email: "",
                password: ""

            },

            formSchema: {

                name: yup.string().trim().required("Sorry, the name is required"),
                surname: yup.string().trim().required("Sorry, the surname is required"),
                email: yup.string().required("Sorry, the email is required").email("Sorry, the email is not valid").trim(),
                password: yup.string().trim()
                    .required("Sorry, the password is required")
                    .min(8, "Password must be at least 8 characters long")
                    .matches(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&_\-])[A-Za-z\d@$!%*?&_\-]+$/, "Your password must contain at least one lowercase letter, one uppercase letter, one number, and one special character")

            },

            submittedUsers: [],

        };

    },

    methods: {

        onSubmit(values, { resetForm }) {

            console.info("The submission was successful");

            this.fetchUserData(values);

            resetForm();

        },

        onInvalidSubmit({ values, errors, results }) {

            console.error("The submission was unsuccessful");

            console.log(values);
            console.log(errors);
            console.log(results);

        },

        visualValidationInput(meta) {

            return {

                'is-valid': meta.valid && meta.touched,
                'is-invalid': !meta.valid && meta.touched

            };

        },

        fetchUserData(userData) {

            const userDataJSON = JSON.stringify(userData);

            // Ciò garantisce che ogni utente venga memorizzato con una chiave unica e impedisce che i dati vengano sovrascritti ogni volta

            const uniqueKey = `user_${Date.now()}`;

            localStorage.setItem(uniqueKey, userDataJSON);
            console.log(localStorage);

            const storedData = localStorage.getItem(uniqueKey);

            if (storedData) {

                const fetchStoredUserData = JSON.parse(storedData);
                // console.log(fetchStoredUserData);

                if (fetchStoredUserData) {

                    this.submittedUsers.push(fetchStoredUserData);
                    console.log(this.submittedUsers);

                }

            }

        },

    },

}

</script>

<template>

    <Form @submit="onSubmit" :validation-schema="formSchema" @invalid-submit="onInvalidSubmit" v-slot="{ meta }">

        <div class="container">

            <div class="row justify-content-center mt-5">

                <div class="mb-3">

                    <label for="name" class="form-label">Name</label>
                    <Field id="name" name="name" v-slot="{ field, meta }">
                        <input type="text" class="form-control" v-bind="field" v-model="form.name"
                            :class="visualValidationInput(meta)" placeholder="Enter your surname" />
                    </Field>
                    <ErrorMessage name="name" class="text-danger fst-italic small-text">
                    </ErrorMessage>

                </div>

                <div class="mb-3">

                    <label for="surname" class="form-label">Surname</label>
                    <Field id="surname" name="surname" v-slot="{ field, meta }">
                        <input type="text" class="form-control" v-bind="field" v-model="form.surname"
                            :class="visualValidationInput(meta)" placeholder="Enter your surname" />
                    </Field>
                    <ErrorMessage name="surname" class="text-danger fst-italic small-text">
                    </ErrorMessage>


                </div>

                <div class="mb-3">

                    <label for="email" class="form-label">Email</label>
                    <Field id="email" name="email" v-slot="{ field, meta }">
                        <input type="email" class="form-control" v-bind="field" v-model="form.email"
                            :class="visualValidationInput(meta)" placeholder="Enter your email" />
                    </Field>
                    <ErrorMessage name="email" class="text-danger fst-italic small-text">
                    </ErrorMessage>

                </div>

                <div class="mb-3">

                    <label for="password" class="form-label">Password</label>
                    <Field id="password" name="password" v-slot="{ field, meta }">
                        <input type="password" class="form-control" v-bind="field" v-model="form.password"
                            :class="visualValidationInput(meta)" placeholder="Enter your password" />
                    </Field>
                    <ErrorMessage name="password" class="text-danger fst-italic small-text">
                    </ErrorMessage>

                </div>

                <div class="text-center">

                    <button :disabled="!meta.valid" type="submit" class="btn btn-primary">Submit</button>

                </div>

            </div>

        </div>

    </Form>


</template>

<style lang="scss" scoped>
.small-text {

    font-size: 0.8rem;
}
</style>