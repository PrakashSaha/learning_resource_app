<template>
    <base-dailog v-if="inputIsInvalid" title="Invalid Input" @close="closePopUp">
        <template #default>
            <p>Unfortunatly, at least one input value is invalid</p>
            <p>Please cheack your input.</p>
        </template>
        <template #actions>
            <base-button @click="closePopUp">okay</base-button>
        </template>
    </base-dailog>
     <base-card>
      <form @submit.prevent="submitData">
        <div class="from-control">
            <label for="title">Title</label>
            <input id="title" name="title" type="text" ref="titleInput">
        </div>
        <div class="from-control">
            <label for="description">Description</label>
            <textarea name="description" id="description" cols="30" rows="3" ref="desInput"></textarea>
        </div>
        <div class="from-control">
            <label for="link">Link</label>
            <input id="link" name="link" type="url" ref="linkInput">
        </div>
        <div>
           <base-button type="submit">Add Resource</base-button>
        </div>
      </form>
     </base-card>
</template>

<script>

import BaseButton from '../UI/BaseButton.vue';
export default{
  components: { BaseButton },
    inject: ['addResource'],
    data(){
        return{
            inputIsInvalid: false,
        }
    },
     methods:{
        submitData(){
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.desInput.value;
            const enteredUrl = this.$refs.linkInput.value;
            if (enteredTitle.trim() ==='' || 
            enteredDescription.trim() === '' || 
            enteredUrl.trim() === ''){
                this.inputIsInvalid = true;
                return;
            }
           this.addResource(enteredTitle,enteredDescription,enteredUrl);
            // Clear the input fields
            this.$refs.titleInput.value = '';
            this.$refs.desInput.value = '';
            this.$refs.linkInput.value = '';  
        },
        closePopUp(){
            this.inputIsInvalid = false;
        }
     }
}
</script>

<style scoped>
label{
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}
input,
textarea{
    display:block;
    width:100%;
    font:inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}
input:focus,
textarea:focus{
    outline:none;
    border-color:#3a0061;
    background-color:#f7ebff;
}
.from-control{
    margin: 1rem 0;
}
</style>