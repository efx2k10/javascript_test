<template>

<div class="row">
  <div class="col s6 offset-s3">
    <h1>Create Task</h1>

    <form @submit.prevent="submitHandler">
      <div class="input-field">
          <input id="title" type="text" class="validate" required v-model="title">
          <label for="title">Title</label>
          <span class="helper-text" data-error="wrong" data-success="right">Введите название таска</span>
      </div>


      <div class="chips" ref="chips"></div>

      <div>
         <textarea id="description" class="materialize-textarea" v-model="description"></textarea>
         <label for="description">description</label>
         <span class="character-counter" style="float: right; font-size: 12px;">{{ description.length }}/2048</span>
      </div>

      <input type="text" class="datepicker" ref="datapicker">

      <button class="btn" type="submit">Create Task</button>

    </form>

  </div>
</div>


  
</template>

<script>

import M from 'materialize-css'

export default {
  name: 'Create',
  data: () => ({
    description:'',
    title:'',
    chips: null,
    date: null
  }),
  mounted() {
 
  this.chips = M.Chips.init(this.$refs.chips, {
    placeholder:'Task TAG'
  })

  this.date = M.Datepicker.init(this.$refs.datapicker, {
      format:'dd.mm.yyyy',
      defaultDate: new Date(),
      setDefaultDate: true
    
  })

  },

  methods: {
    submitHandler() {
      const task = {
        title : this.title,
        description : this.description,
        id : Date.now(),
        status : 'active',
        tags : this.chips.chipsData,
        date : this.date.date

      }

      console.log(task)

    }
  },

  destroyed() {
    if (this.date && this.date.destroy) {
      this.date.destroy()
    }

    if (this.chips && this.chips.destroy) {
      this.chips.destroy()
    }


  }


}



</script>
