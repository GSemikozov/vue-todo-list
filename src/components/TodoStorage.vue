<script type="text/javascript">
    const STORAGE_KEY = 'vue-js-todo'
    const todoStorage = {
        fetch () {
            var todoItems = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
            return todoItems
        },
        save (item) {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(item))
        },
        deleteItem (item) {
            localStorage.removeItem(item)
        }
    }
    export default todoStorage
</script>