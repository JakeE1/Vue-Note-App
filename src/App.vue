<template>
<div class="wrapper">

  <div class="wrapper-content">
    <section>
      <div class="container">
        

        <message v-if="message" :message="message"></message>

        <!-- new note -->
        <newNote :note="note"  @addNote="addNote" />

        <!-- title -->
        <div class="note-header title">
          <h1> {{ title }} </h1>

          <!-- search -->
           <search @search="search = $event" :value="search" placeholder="Find your note" />

            <!-- icons-cotrol -->
          <div class="icons">
            <svg :class="{ active: grid }" @click="grid = true"  x="0px" y="0px"
              width="24px" height="24px" viewBox="0 0 124 124" style="enable-background:new 0 0 124 124; cursor: pointer;" xml:space="preserve">
            <g>
              <path d="M112,6H12C5.4,6,0,11.4,0,18s5.4,12,12,12h100c6.6,0,12-5.4,12-12S118.6,6,112,6z"/>
              <path d="M112,50H12C5.4,50,0,55.4,0,62c0,6.6,5.4,12,12,12h100c6.6,0,12-5.4,12-12C124,55.4,118.6,50,112,50z"/>
              <path d="M112,94H12c-6.6,0-12,5.4-12,12s5.4,12,12,12h100c6.6,0,12-5.4,12-12S118.6,94,112,94z"/>
            </g>
          </svg>

          <svg :class="{ active: !grid }"  @click="grid = false"   x="0px" y="0px" width="24px" height="24px"
            viewBox="0 0 290 290" style="enable-background:new 0 0 290 290; cursor: pointer;" xml:space="preserve">
            <g>
              <path d="M165,0v125h125V0H165z M260,95h-65V30h65V95z"/>
              <path d="M0,125h125V0H0V125z M30,30h65v65H30V30z"/>
              <path d="M0,290h125V165H0V290z M30,195h65v65H30V195z"/>
              <path d="M165,290h125V165H165V290z M195,195h65v65h-65V195z"/>
            </g>

          </svg>
          </div>
        </div>

        <!-- note list -->

        <notes :notes="notesFilter" @remove="removeNote" :grid="grid" />
        
      </div>
    </section>
  </div>



</div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/addNote.vue'
import notes from '@/components/notes.vue'
import search from '@/components/Search.vue'

export default {
  components: {
    message, notes, newNote, search
  },
  data () {
    return {
      title: "Notes App",
      grid: true,
      search: '',
      message: null,
       note: {
        title: '',
        descr: '',
        type: '#f7f7f7'
       },
       notes: [
           {
               title: 'First Note',
               descr: 'Description for first note',
               type: '#f7f7f7',
               date: new Date(Date.now()).toLocaleString() 
           },
            {
                title: 'Second Note',
                descr: 'Description for first note',
                type: '#f7f7f7',
                date: new Date(Date.now()).toLocaleString() 
            },
            {
                title: 'Third Note',
                descr: 'Description for first note',
                type: '#f7f7f7',
                date: new Date(Date.now()).toLocaleString() 
            },
       ]
    }
  },
  computed: {
      notesFilter(){
        let arr = this.notes,
         search = this.search;
         if (!search) return arr;
         
         search = search.trim().toLowerCase(); 
         //Filter
         arr = arr.filter(function(item){
            if(item.title.toLowerCase().indexOf(search) !== -1){
              return item;
            }       
         });
         return arr;
      }  
    },
  
  methods: {
        addNote() {
            let {title, descr, type} = this.note;

            if(title === '') {
                this.message = 'WARNING: title can\'t be blank';
                return false;
            }

           this.notes.push ({
               title,
               descr,
               type,
               date: new Date(Date.now()).toLocaleString() 
           });
           
           this.message = null;
           this.note.title = '';
           this.note.descr = '';
           this.note.type = '#f7f7f7';
           
        },
        removeNote(index){
            this.notes.splice(index, 1);
        }
    }
  }

</script>

<style>
</style>
