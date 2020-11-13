<template>
    <div class="new-note">
        <label>Title</label>
        <div class="new-note header">
            <input v-model="note.title" type="text" >
            <div class="importance">
                <div @click="setImportance('#f7f7f7')" data-importance="0">
                    common
                </div>
                <div @click="setImportance('yellow')" data-importance="1">
                    important
                </div>
                <div @click="setImportance('red')" data-importance="2">
                    most important
                </div>
            </div>
        </div>
            
            <label>Description</label>
            <textarea v-model="note.descr"></textarea>
            <button class="btn btnPrimary" @click="addNote">New Note</button>
        </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        }
    },
    methods: {
        addNote(){
            this.$emit('addNote', this.note)
        },
        setImportance: function(text){
            this.note.type = `${text}`;
        }
    }
}
</script>

<style lang="scss" scoped>
    .new-note {
        text-align: center;
        &.header {
            display: flex;
            justify-content: space-between;
        }
    }
    .importance{
        display: flex;
        justify-content: space-between;
        cursor: pointer;
        
        div{
            margin: 0 10px;
            padding: 10px;
            width: 300px;
            height: 54px;
            
            

            border: 2px solid blue;
        }
    }
    button {
        margin: 15px 0;
    }
</style>
