<template>
  <div class="hello">
    email><input type='text' v-model='email' />password><input type='text' v-model='password' /><button @click='login'>Login</button>
  </div>
</template>

<script>
export default {
  name: 'Avtoriz.vue',
 data() {
  return {
    email: '',
    password:''
  }
},
methods: {
  login () {
    console.log('i am Avtoriz!!', this.email, this.password);
    this.$emit('login', {
      email: this.email,
      password: this.password
    });
  }
}
}
</script>


