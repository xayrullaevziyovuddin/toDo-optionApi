<template>
    <Transition name="modal">
        <div class="modal" @click="$emit('send', !modalShow), text = '', title = ''">
            <div class="modal__block" @click.stop="">

                <h2 class="modal__block-title">
                    {{ edit ? $t('addNote') : $t('changeNote') }}
                </h2>

                <div class="modal__block-inputs">

                    <label>
                        <span>Title</span>
                        <input type="text" v-model="title" :placeholder="info">
                    </label>

                    <label>
                        <span>Content</span>
                        <textarea v-model="text">

                    </textarea>
                    </label>

                </div>
                <div class="modal__block-btns">
                    <button class="modal__block-btns-btn del"
                        @click="$emit('send', !modalShow), text = '', title = ''">{{$t('cancel')}}</button>
                    <button v-show="edit" class="modal__block-btns-btn edit" @click="addNote">{{$t('add')}}</button>
                    <button v-show="!edit" class="modal__block-btns-btn edit" @click="editNote">{{$t('change')}}</button>
                </div>
            </div>
        </div>
    </Transition>
</template>

<script>
import { v4 as uuidv4 } from 'uuid'

export default {


    props: {
        modalShow: {

            typeof: Boolean
        },
        edit: {

            typeof: Boolean

        },
        editedNote: {

            typeof: Object
        }
    },
    data() {
        return {
            title: '',
            text: '',
            info: '',
            id: 0

        }
    },

    methods: {

        closeModal() {
            this.$emit('close')

        },

        addNote() {

            const note = {
                id: uuidv4(),
                title: this.title,
                text: this.text,
                data: new Date().toLocaleDateString()

            }
            if (this.title.length > 0 && this.text.length > 0) {

                this.$emit('addNote', note)

                this.text = ''
                this.title = ''
                this.closeModal()
                this.info = ''
            } else {
                this.info = 'Поле пустое'

            }


        },

        editNote() {

            if (this.title.length > 0 && this.text.length > 0) {

                const newEditedNote = {
                    id: this.editedNote.id,
                    title: this.title,
                    text: this.text,
                    data: new Date().toLocaleDateString()


                }

                this.$emit('newNote', newEditedNote)
                this.text = ''
                this.title = ''
                this.closeModal()
                this.info = ''
            }else {
                this.info = 'Поле пустое'

            }

        }
    },
}
</script>

