<template lang="html">
  <div class="">
    <section class="section">
      <div class="container">
        <form @submit.prevent="submitForm" class="panel">

        <div class="panel">
          <p class="panel-heading title">
            Sign Up For My Web App
          </p>
          <p v-for"item in formInputs" v-if="item.type !== 'select' && item.type !== 'textarea' " class="control has-icon has-icon-left">
            <i class="fa fa-user-o" aria-hidden="true"></i>
            <input v-model="formValues[formInputs.id]" class="input" type="text" :placeholder="item.label">
          </p>
          <p v-for"item in formInputs" v-if="item.type === 'select'" class="control has-icon has-icon-left">
            <span class="select is-fullwidth">
              <select v-model="formValues[formInputs.id]" :placeholder="item.label">
                <option v-for="option in item.options" value="">{{ option.label }}</option>
              </select>
            </span>
          </p>

          <p v-for="item in formInputs" v-if="item.type === 'textarea' " class="control has-icon has-icon-left">
            <i class="fa fa-comments-o" aria-hidden="true"></i>
            <textarea class="textarea input" :placeholder="item.label" v-model="formValues[formInputs.id]"></textarea>
          </p>

          <p class="control is-fullwidth">
            <button @click="submitForm(formValues)" class="button is-fullwidth is primary">Submit</button>
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
      apiUrl,
      formImputs: [],
      formValues: [],
    };
  },

  mounted() {
    this.getData();
  },

  methods: {
    getdata() {
      fetch(apiUrl)
        .then((r) => r.json())
        .then((formInputs) => {
          this.formInputs = formInputs;
        });
    },
    submitForm(formValues) {
      fetch('http://tiny-tn.herokuapp.com/collections/form-dustin', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.formValues)
        })
        .then(() => {
          this.formValues = formValues;
          console.log(formValues);
        });
    },
  },
};
</script>
