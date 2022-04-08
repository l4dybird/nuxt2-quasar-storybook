<script setup lang="ts">
import { ref } from '@nuxtjs/composition-api';

const name = ref(null);
const age = ref(null);
const accept = ref(false);
const refName = ref();
const refAge = ref();
const refAccept = ref();
const refFrom = ref();
const onSubmit = () => {
  console.log('click');
};

const onValidate = (): void => {
  refFrom .value.$children.map(
    (e: { validate?: any; }) => Object.keys(e).includes('validate') ? e.validate() : ''
  );
};

const onReset = () => {
    name.value = null
    age.value = null
    accept.value = false
}
</script>

<template>
  <div id="q-app">
    <div class="q-pa-md" style="max-width: 400px">
      <q-form
        ref="refFrom"
        class="q-gutter-md"
        @submit="onSubmit"
        @reset="onReset"
      >
        <q-input
          ref="refName"
          v-model="name"
          filled
          label="Your name *"
          hint="Name and surname"
          lazy-rules
          :rules="[val => val && val.length > 0 || 'Please type something']"
        ></q-input>

        <q-input
          ref="refAge"
          v-model="age"
          filled
          type="number"
          label="Your age *"
          lazy-rules
          :rules="[
            val => val !== null && val !== '' || 'Please type your age',
            val => val > 0 && val < 100 || 'Please type a real age'
          ]"
        ></q-input>

        <q-toggle ref="refAccept" v-model="accept" label="I accept the license and terms"></q-toggle>

        <div>
          <q-btn label="Submit" type="submit" color="primary"></q-btn>
          <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm"></q-btn>
        </div>
        <q-btn label="hoge" color="primary" @click="onValidate"></q-btn>
      </q-form>
    </div>
  </div>
</template>