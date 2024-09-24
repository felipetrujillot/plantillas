<template>
  <editor-content
    class="min-h-20 px-3 py-2 border rounded-md"
    :editor="editor"
  />
</template>

<script setup>
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

const descripcion = defineModel()

const editor = useEditor({
  content: descripcion.value,
  extensions: [StarterKit],
  editorProps: {
    attributes: {
      class: `dark:prose-invert prose prose-xs sm:prose lg:prose-lg xl:prose-xl focus:outline-none prose-p:leading-normal prose-p:m-0 prose-a:leading-normal prose-a:m-0 prose-h1:leading-normal prose-h1:m-0 prose-h2:leading-normal prose-h2:m-0 prose-h3-a:leading-normal prose-h3:m-0 prose-h4-a:leading-normal prose-h4:m-0 prose-h5-a:leading-normal prose-h5:m-0 prose-h6-a:leading-normal prose-h6:m-0 prose-li-a:leading-normal prose-li:m-0 prose-ul-a:leading-normal prose-ul:m-0`,
    },
  },
  onUpdate: () => {
    descripcion.value = editor.value.getHTML()
  },
})
</script>
