<script setup>
import { useForm } from 'vee-validate';
import * as yup from 'yup';
import InputText from 'primevue/inputtext';
import Dropdown from 'primevue/dropdown';
import Button from 'primevue/button';
import Checkbox from 'primevue/checkbox';

const schema = yup.object({
  email: yup.string().required().email().label('Email address'),
  fullName: yup.string().required().label('Full name'),
  password: yup.string().required().min(6).label('Password'),
  passwordConfirm: yup
    .string()
    .oneOf([yup.ref('password')], 'Passwords must match'),
  terms: yup
    .boolean()
    .required()
    .isTrue('You must agree to terms and conditions')
    .label('terms agreement'),
  type: yup.string().required().label('Account type'),
});

const { defineComponentBinds, handleSubmit, resetForm, errors } = useForm({
  validationSchema: schema,
});

const fullName = defineComponentBinds('fullName');
const email = defineComponentBinds('email');
const password = defineComponentBinds('password');
const passwordConfirm = defineComponentBinds('passwordConfirm');
const terms = defineComponentBinds('terms');
const type = defineComponentBinds('type');

const onSubmit = handleSubmit((values) => {
  console.log('Submitted with', values);
});

const options = ['Enterprise', 'Pro', 'Freelance'].map((o) => ({
  name: o,
  value: o.toLowerCase(),
}));
</script>

<template>
  <div class="border max-w-lg mx-auto mt-12">
    <form @submit="onSubmit" class="border flex flex-col gap-4">
      <div>
        <label for="fullName">Full name</label>
        <InputText
          v-bind="fullName"
          :class="{ 'border-red-500': errors.fullName }"
        />
        <small id="fullName-help" class="text-red-500">
          {{ errors.fullName }}
        </small>
      </div>

      <div>
        <label for="email">Email</label>
        <InputText
          v-bind="email"
          aria-describedby="email-help"
          type="email"
          :class="{ 'border-red-500': errors.email }"
        />
        <small id="email-help" class="text-red-500">{{ errors.email }}</small>
      </div>

      <div>
        <label for="password">Password</label>
        <InputText
          v-bind="password"
          aria-describedby="password-help"
          type="password"
          :class="{ 'border-red-500': errors.password }"
        />
        <small id="password-help" class="text-red-500">
          {{ errors.password }}
        </small>
      </div>

      <div>
        <label for="passwordConfirm">Password Confirmation</label>
        <InputText
          v-bind="passwordConfirm"
          aria-describedby="password-confirm-help"
          type="password"
          :class="{ 'border-red-500': errors.passwordConfirm }"
        />
        <small id="password-confirm-help" class="text-red-500">
          {{ errors.passwordConfirm }}
        </small>
      </div>

      <div>
        <label for="type">Type</label>
        <Dropdown
          v-bind="type"
          :options="options"
          optionLabel="name"
          optionValue="value"
          :class="{ 'border-red-500': errors.type }"
          placeholder="Select a type"
        />

        <small id="email-help" class="text-red-500">{{ errors.type }}</small>
      </div>

      <div class="flex flex-col gap-2">
        <div class="flex gap-2 flex-row-reverse justify-end">
          <label for="chbx">I've read and accept the terms & conditions.</label>
          <Checkbox
            id="chbx"
            v-bind="terms"
            :class="{ 'border-red-500': errors.terms }"
            binary
            aria-describedby="chbx-error"
          />
        </div>

        <small class="text-red-500" id="chbx-error">
          {{ errors.terms || '&nbsp;' }}
        </small>
      </div>


      <div class="flex gap-4">
        <Button label="Submit" type="submit" />

        <Button
          label="Reset"
          type="button"
          @click="resetForm"
          class="bg-gray-500"
        />
      </div>
    </form>
  </div>
</template>
