<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" v-on:close="confirmError">
    <template v-slot:default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a couple of
        characters.
      </p>
    </template>
    <template v-slot:actions>
      <base-button v-on:click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form v-on:submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input ref="titleInput" id="title" name="title" type="text" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          ref="descInput"
          id="description"
          name="description"
          rows="3"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Resource link</label>
        <input ref="linkInput" id="link" name="link" type="url" />
      </div>
      <div class="form-control">
        <base-button type="submit">Add resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
  inject: ['addResource'],
  data: function() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      } else {
        this.addResource(enteredTitle, enteredDescription, enteredUrl);
      }
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
