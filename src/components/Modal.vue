<!-- https://github.com/Gadrawingz/Vue-Modal-App -->
<template>
    <!-- Click event modifiers -->
    <div class="backdrop" @click.self="closeModal">
        <div class="modal" :class="{sale: theme === 'sale'}">
            <h1> {{ header }} </h1>
            <p>  {{ content }} </p>
        </div>
    </div>
</template>


<!-- First Way: (1) Using Props -->
<script>
export default {
    props: ['header', 'content', 'theme'],
    methods: {
        closeModal() {
            this.$emit('close')
        }
    }
}
</script>



<style>
.modal {
    width: 100px;
    min-width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: white;
    border-radius: 8px;
}

.backdrop {
    top: 0;
    position: fixed;
    background: rgba(0, 0, 0, 0.8);
    width: 100%;
    height: 100%;
}

.modal h1 {
    color: #03cfb4;
    border: none;
    padding: 0;
}

.modal p {
    font-style: normal;
}

/* When its sale */
.modal.sale {
    background: brown;
    color: white;
}

.modal.sale h1 {
    color: white;
}

/* When its dark */
.modal.dark {
    background: #000000;
    color: white;
}

.modal.dark h1 {
    color: white;
}

</style>