<script>
import axios from 'axios';
export default {
    props: {
        modelValue: { type: String, default: "" },
    },
    emits: ["submit", "update:modelValue"],
    methods: {
        updateModelValue(e) {
            this.$emit("update:modelValue", e.target.value);
        },
        async submit() {
            this.$emit("submit");
            try {
                const response = await axios.get('/', {
                    params: {name: this.modelValue}
                });
                console.log(response.data);
            } catch(error) {
                console.log(error);
            }
        },
    },
};
</script>

<template>
<div class="input-group">
    <input
        type="text" class="form-control" placeholder="Nhập thông tin cần tìm"
        :value="modelValue"
        @input="updateModelValue"
        @keyup.enter="submit"
    />
    <div class="input-group-append">
        <button class="btn btn-outline-secondary" type="button" @click="submit">
            <i class="fas fa-search"></i> Tìm kiếm
        </button>
    </div>
</div>
</template>
