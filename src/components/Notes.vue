<template>
    <div class="notes">
        <div class="container">

            <div class="notes__top">
                <h2 v-if="notes.length > 0" class="notes__top-title">{{$t('allNotes')}}: {{ notes.length }}</h2>
                <h2 v-if="notes.length == 0" class="notes__top-title">{{$t('noNotes')}} (</h2>
                <button  v-if="notes.length > 0" @click="view = !view" class="notes__top-btn">

                    <img v-show="view" src="@/assets/images/list.svg" alt="">
                    <img v-show="!view" src="@/assets/images/layout.svg" alt="">
                    <span>{{ view ? $t('list') : $t('grid') }}</span>

                </button>
            </div>

            <div class="notes__list" :class="{active: !view}">
 

                <Note @editNote="$emit('editNote',note.id)"   @delNote="$emit('delNote',note.id)"   v-for="note in notes" :key="note.id"    :note="note" :view="view" />


            </div>

        </div>
    </div>
</template>

<script>
import Note from './Note.vue';

export default {

props:{

notes:{
 typeof:Array

}



},

    data() {
        return {
            view: true,
        };
    },
    components: { Note },


 
}
</script>

