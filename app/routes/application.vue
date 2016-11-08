<template lang="html">
  <div class="">
    <section class="section">
      <div class="container">
        <form @submit.prevent="submitForm" class="panel">

        <div class="panel">
          <p class="panel-heading title">
            Sign Up For My Web App
          </p>

          <div class="panel-block">
            <p class="control has-icon has-icon-left">
              <i class="fa fa-user-o" aria-hidden="true"></i>
              <input class="input" type="text" placeholder="item.label">
            </p>
            <p class="control has-icon has-icon-left">
              <span class="select is-fullwidth">
                <select placeholder="item.label">
                  <option value="">{O label}</option>
                  <option value="">{O label}</option>
                </select>
              </span>
            </p>

            <p class="control has-icon has-icon-left">
              <i class="fa fa-comments-o" aria-hidden="true"></i>
              <textarea class="textarea input"></textarea>
            </p>
          </div>

          <p class="panel-block">
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
      formInputs: [],
      formValues: {},
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
