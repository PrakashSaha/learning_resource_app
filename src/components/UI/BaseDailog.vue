<template>
    <div @click="$emit('close')"></div>
    <dialog open @click.stop> 
        <header>
            <slot name="header">
                <h2>{{ title }}</h2>
            </slot>
        </header>
        <section>
            <slot></slot>
        </section>
        <menu>
            <slot name="actions">
                <base-button @click="$emit('close')">Close</base-button>
            </slot>
        </menu>
    </dialog>
</template>

<script>
export default{
    props:{
        title:{
            type: String,
            required: false
        }
    },
    emits: ['close']
};
</script>

<style scoped>
.overlay {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: rgba(0, 0, 0, 0.5);
}
.dialog-box {
    position: relative;
    background: white;
    padding: 20px;
    max-width: 500px;
    margin: 50px auto;
    border-radius: 8px;
}
</style>