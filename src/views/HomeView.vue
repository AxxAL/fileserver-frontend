<script>
export default {
    data() {
        return {
            files: Array
        }
    },

    methods: {
        async getFiles() {
            await fetch("https://api-files.axxal.net/list")
                .then(async response => {
                    response = await response.json();
                    this.files = response.fileList;
                });
        }
    },

    created() {
        this.getFiles();
    }
}
</script>

<template>
    <main>
        <h1 class="is-size-1 mt-5">Files:</h1>
        <ul>
            <li v-for="file in files" v-bind:key="file.fileName" class="box">
                <a :href="file.downloadLink">{{ file.fileName }}</a>
                <p class="has-text-grey-light">{{ file.fileSize }}</p>
            </li>
        </ul>
    </main>
</template>