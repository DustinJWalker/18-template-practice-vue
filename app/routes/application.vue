<template lang="html">
  <div class="">
    <section class="section">
      <div class="container">
        <form @submit.prevent="submitForm(formData)" class="panel">

        <div class="panel">
          <p class="panel-heading title">
            Sign Up For My Web App
          </p>

          <div class="panel-block">
            <p class="control has-icon has-icon-left" v-for="input in formInputs">
              <template v-if="input.type === 'select'">
                <span class="select is-fullwidth">
                  <select v-model="formData[input.id]">
                    <option :value="undefined">{{ input.label }}</option>
                    <option v-for="option in input.options">{{ option.label }}</option>
                  </select>
                </span>
              </template>
              <template v-else>
                <template v-if="input.type === 'textarea' ">
                  <i class="fa" :class="input.icon" aria-hidden="true"></i>
                  <textarea class="textarea input" :placeholder="input.label" v-model="formData[input.id]"></textarea>
                </template>

                <template v-else>

                  <i class="fa" :class="input.icon" aria-hidden="true"></i>
                  <input class="input" type="text" :placeholder="input.label" v-model="formData[input.id]">
                </template>
              </template>
            </p>
          </div>

          <p class="panel-block">
            <button class="button is-fullwidth is-primary">Submit</button>
          </p>

        </div>
      </form>

      </div>
    </section>
  </div>
</template>

<script>
const apiUrl = 'http://json-data.herokuapp.com/forms'
export default {
  data() {
    return {
      apiUrl: 'apiUrl',
      formInputs: [],
      formData: {},
    };
  },

  mounted() {
    this.getData();
  },

  methods: {
    getData() {
      fetch(apiUrl)
        .then((r) => r.json())
        .then((formInputs) => {
          this.formInputs = formInputs;
        });
    },
    submitForm(inputs) {
      fetch('http://tiny-tn.herokuapp.com/collections/form-dustin', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(inputs)
        })
        .then(() => {
          console.log(inputs);
        });
    },
  },
};
</script>
