<template>
    <!-- This complex modal we need to use Slots -->
    <div class="backdrop" @click.self="closeModal">
        <div class="modal" :class="{dark: theme === 'dark'}">
            <!-- Default content:Will only show up if we dont have default slot-->
            <slot>Default Content</slot>
            <div class="some-links">
                <slot name="links"></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['theme'],
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
    color: green;
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

.modal.sale h1,
.some-links,
.some-links a
 {
    color: white;
}

/* When its dark */
.modal.dark {
    border: 1px solid lightcyan;
    background: #000000;
    color: white;
}

.modal.dark h1 {
    color: white;
}


/* Hyperlink styles */
.some-links {
    text-align: center;
    margin: 30px 0 10px;
    color: #333;
}

.some-links a{
    color: lightgoldenrodyellow;
    padding: 8px;
    border: 1px solid lightskyblue;
    border-radius: 4px;
    text-decoration: none;
    margin: 10px;
}

</style>