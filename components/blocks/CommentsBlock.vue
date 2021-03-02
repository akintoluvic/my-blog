<script>
export default {
    async fetch() {
        this.comments = await fetch(
            `https://dev.to/api/comments?a_id=${this.$route.params.article}`
        ).then((res) => res.json())
    },
    fetchOnServer: false

}
</script>