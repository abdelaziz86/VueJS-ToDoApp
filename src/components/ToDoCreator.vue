<template>
    <div class="input-wrap">
        <input type="text" v-model="todoState.todo" />
        <button @click="createToDo()">Create</button>
        

    </div>
        <pre>{{ todoState.todo }}</pre>

    <!-- <p v-if="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p> -->
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
</template>

<script>
import { reactive, ref, defineEmits } from "vue";
const emit = defineEmits(["createToDo"]);

export default {
    data() {
        return {
            todoState: reactive({
                todo: "",
                invalid: null,
                errMsg : ""
            })

             
        };
    }, 
    methods: {
        createToDo() {
             this.todoState.invalid = false;
            if (this.todoState.todo !== "") {
                this.$emit("createToDo", this.todoState.todo);
                this.todoState.todo = "";
                return;
            }
            this.todoState.invalid = true;
            this.todoState.errMsg = "Todo is required";
        }
    }
};


</script>

<style lang="scss" scoped>
.input-wrap {
    display: flex;
    transition: 250ms ease;
    border: 2px solid #41b080;

    &:focus-within {
        box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
            0 -2px 4px -2px rgb(0 0 0 / 0.1);
    }

    input {
        width: 100%;
        padding: 8px 6px;
        border: none;

        &:focus {
            outline: none;
        }
    }

    button {
        padding: 8px 16px;
        border: none;
    }
}
</style>
