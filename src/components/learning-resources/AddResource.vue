<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="con">
        <template #default>
            <p>Unfortunately, at least one input value is Invalid.</p>
            <p>Please check all inputs and make sure you enter at least one character for all inputs</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" name="title" type="text" ref="titleInput">
            </div>
            <div class="form-control">
                <label for="description">description</label>
                <textarea 
                id="description" 
                name="description" 
                type="text" 
                rows="3"
                ref="descInput"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" ref="linkInput">
            </div>
            <div class="form-control">
                <base-button type="submit" >Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default{
    inject: ['addResource'],
    data(){
        return{
            inputIsInvalid: false
        }
    },
    methods: {
        submitData(){
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.descInput.value;
            const enteredLink = this.$refs.linkInput.value;

            if(enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim() === ''){
                this.inputIsInvalid = true;
                return;
            }

            this.addResource(enteredTitle, enteredDescription, enteredLink);
        },
        confirmError(){
            this.inputIsInvalid = false
        }
    }
}
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