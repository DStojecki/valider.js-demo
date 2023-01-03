<template>
    <form class="valider-form">
        <h3>Type something in inputs</h3>
        <div class="valider-form__group">
            <label for="">First name</label>
            <input data-required data-minlength="3" class="my-input" />
        </div>
        <div class="valider-form__group">
            <label for="">Select something</label>
            <select data-required data-event="change" class="my-input">
                <option value="" selected></option>
                <option value="Some">Some</option>
                <option value="Thing">Thing</option>
            </select>
        </div>
        <div class="valider-form__group">
            <label for="">Custom validation input</label>
            <input
                data-custom="^[a-zA-Z]+$"
                data-custom-err="Custom err based on regexp (in this case letters only)"
                class="my-input"
            />
        </div>
        <div class="valider-form__group">
            <label for="">Age</label>
            <input
                data-required
                data-numberonly
                data-maxlength="3"
                class="my-input"
            />
        </div>
        <div class="valider-form__group">
            <label for="">Are you sure?</label>
            <div>
                <input
                    data-event="change"
                    data-required
                    type="checkbox"
                    class="my-input"
                />
                <label for="">Yes</label>
            </div>
        </div>
        <div class="valider-form__group">
            <label for="">Are you sure radio?</label>
            <div>
                <input
                    id="1"
                    data-event="change"
                    data-required
                    type="radio"
                    class="my-input"
                    name="radioGroup"
                    value="test1"
                />
                <label for="1">Yes</label>
                <input
                    id="2"
                    data-event="change"
                    data-required
                    type="radio"
                    class="my-input"
                    name="radioGroup"
                    value="tnop"
                />
                <label for="2">No</label>
            </div>
        </div>
        <button
            @click.prevent="check(valider)"
            class="valider-form__submit submit"
        >
            Submit
        </button>
    </form>
</template>

<script setup>
import { Valider } from "valider.js";
import { reactive, onMounted } from "vue";

const data = reactive({});

onMounted(() => {
    const config = {
        selector: ".my-input",
        addValidClass: true,
        validateOn: "keyup",
    };

    data.valider = new Valider(config);
});

const check = () => {
    if (data.valider.check()) {
        console.log("Validation successfull");
    } else {
        console.log("Validation failed!");
    }
};
</script>

<style scoped>
h3 {
    font-weight: 500;
    color: #333;
}
</style>
