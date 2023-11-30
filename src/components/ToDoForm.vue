<template>
    <form @submit.prevent="onSubmit">
        <label for="new-todo-input">What are you doning?</label>
        <input type="text"
            id="new-todo-input"
            name="new-todo"
            autocomplete="off"
            v-model.lazy.trim="label"  />
        <button type="submit">More</button>
    </form>
</template>

<script>
    export default {
        methods: {
            onSubmit() {
                console.log("onSubmit method called");
                if(this.label === "") {
                    return;
                };
                this.$emit("todo-added", this.label);
                this.label = "";
            },
        },
    data() {
        return {
            label: "",
        };
    },
    };
</script>