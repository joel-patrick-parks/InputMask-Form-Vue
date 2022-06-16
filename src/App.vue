<template>
  <div class="form-control">
  <div class="form-header">
    <span>User Information</span>
  </div>
  <form class="form-body" v-on:submit="onSubmit">
    <div class="form-element">
      <wj-input-mask ref="name" id="name" :placeholder="'Name'"></wj-input-mask>
    </div>
    <div class="form-element">
      <wj-input-mask ref="email" id="email" :placeholder="'Email'"></wj-input-mask>
    </div>
    <div class="form-element">
      <wj-input-mask ref="phone" id="phone" :mask="'000-000-0000'" :placeholder="'Phone Number'" :isRequired="false" :promptChar="'#'" :value="''" :valueChanged="validateMask"></wj-input-mask>
    </div>
    <div class="form-element">
      <wj-input-mask ref="social" id="social" :mask="'000-00-0000'" :placeholder="'Social Security Number'" :isRequired="false" :promptChar="'*'" :value="''" :valueChanged="validateMask"></wj-input-mask>
    </div>
    <div class="form-footer">
      <button class="form-button" type="submit">Submit</button>
    </div>
  </form>
</div>
</template>

<script>
import '@grapecity/wijmo.styles/themes/wijmo.theme.material.css';
import * as wjcCore from '@grapecity/wijmo';
import * as wjcInput from '@grapecity/wijmo.vue2.input';

export default {
  name: 'App',
  components: {
    'wj-input-mask': wjcInput.WjInputMask
  },
  methods: {
    onSubmit: function() {
      if(this.isFormComplete()) {
        // Display user info on form submission
        alert('User Information:\nName: ' + this.$refs.name.control.value + 
          '\nEmail: ' + this.$refs.email.control.value + '\nPhone Number: ' + this.$refs.phone.control.value + 
          '\nSSN: ' + this.$refs.social.control.value);
      }
    },
    validateMask: function(ctrl) {
      wjcCore.toggleClass(ctrl.hostElement, 'state-invalid', !ctrl.maskFull);
    },
    isFormComplete: function() {
      if(this.$refs.name.control.value !== '' && this.$refs.email.control.value !== '' && this.$refs.phone.control.maskFull && this.$refs.social.control.maskFull) {
        return true;
      }
      return false;
    }
  }
}
</script>

<style>
.form-control {
    position: absolute;
    width: 400px;
    height: 300px;
    z-index: 15;
    top: 50%;
    left: 50%;
    margin: -150px 0 0 -200px;
    border-radius: 15px;
    box-shadow: 1px 0 5px -2px rgb(90, 90, 90);
    text-align: center;
}

.form-header {
    height: 50px;
    width: 100%;
    line-height: 50px;
    border-top-left-radius: 15px;
    border-top-right-radius: 15px;
    background: rgb(100, 100, 252);
    font-weight: bold;
    font-size: larger;
    color: white;
}

.form-body {
    height: 100%;
    position: relative;
}

.form-element {
    text-align: center;
    margin-top: 15px;
    width: 100%;
}

.form-footer {
    position: absolute;
    bottom: 75px;
    right: 2px;
    height: 50px;
    width: 100%;
}

.form-button {
    float: right;
    margin-top: 10px;
    margin-right: 10px;
    height: 40px;
    width: 100px;
    border-radius: 10px;
    border: 1px solid black;
    background: rgb(100, 100, 252);
    color: white;
    font-size: 16px;
}

.form-button:hover {
    cursor: pointer;
    background: rgb(140, 140, 255);
}

.state-invalid {
    color: red;
}
</style>
