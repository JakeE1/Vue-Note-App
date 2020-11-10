

<template>
<div class="notes">
    <div class="note" :class="{full: !grid}" v-for="(note, index) in notes" :key="index" :style="{border:`3px solid ${notes[index].type}`}">
        <div class="note-header">
            <p>{{ note.title }}
                <input
                v-if="note.edit"
                v-model="note.title"
                @blur="note.edit = false; $emit('update')"
                @keyup.enter="note.edit=false; $emit('update')"
                v-focus
            ><div v-else>
                <label @click="note.edit = true;"> {{note.title}} </label>
            </div>
            

            </p>
            <p style="cursor: pointer;" @click="remove(index)">x</p>
        </div>

        
        <div class="note-body">
            <p>{{ note.descr }}</p> 
            <span>{{ note.date }}</span> 
        </div>
    </div>
</div>
</template>

<script>
export default {

    props: {
        notes: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    },
    data () {
      return {
    editedTodo: null,
    message: 'Hello Vue.js!'
  }
  },
    /* data: {
        styleObject: {
                border:`2px solid ${this.props.notes[index].type}`
        }
    },
    } */
    /* computed:{
        styleObject: function(index){
            return {
                border:`2px solid ${this.notes[index].type}`
        }
        }
    }, */
    /* data: {
        classObject: {
            /* full: !this.grid, 
            white: notes[index].type == 0,
            yellow: notes[index].type == 1,
            red: notes[index].type == 2,
        }
    }*/
    methods: {
        remove(index){
        this.$emit('remove', index);
        
        },
        editTodo(todo){
        this.editedTodo = todo;
    }
    },
    directives: {
    focus: {
      inserted (el) {
        el.focus()
      }
    }
  }
}
</script>

<style lang="scss">
    .notes {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 40px 0;   
    }
    .note {
        width: 48%;
        
        padding: 18px 10px;
        margin-bottom: 10px;
        border-radius: 15px;
        transition: all .25s cubic-bezier(0.2, 0.085, 0.47, 1);
        &.full {
            width: 100%;
        }
        &.yellow {
            background: chocolate;
        }
    }

    .note:hover {
        box-shadow: 0px 0px 15px -1px rgba(0,0,0,0.71);
        transform: translate(0, -6px);
        transition-delay: 0s !important;
    }

    .note-header{
        display: flex;
        align-items: center;
        justify-content: space-between;
        &.title{
            font-size: 25px;
            font-weight: bold;
            margin: 30px 0;
        }
        p {
            color: blue;
            font-size: 22px;
        }
        svg {
            margin-right: 5px;
            &.active {
                box-shadow: 0px 10px 0px -5px #FFFFFF, 0px -10px 0px -5px #FFFFFF, 10px 0px 0px -5px #FFFFFF, -10px 0px 0px -5px #FFFFFF, 0px 0px 0px 5px #1100ff, 5px 0px 21px -7px rgba(0,0,0,0);
            }
            &:last-child {
                margin-right: 0px;
            }
        }
    }

    .note-body{
        p {
            margin: 20px 0;
        }
        span {
            font-size: 14px;
            color: rgb(127, 127, 212)
        }
    }



</style>

