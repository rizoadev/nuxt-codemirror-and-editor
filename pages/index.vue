<template>
  <div id="app">
    <vue-editor v-model="content" :editor-options="editorSettings">
    </vue-editor>
    iki html
    <htmlX :message="content"></htmlX>
    <ClientOnly>
      <editor :code="content"></editor>
    </ClientOnly>
    iki html
  </div>
</template>

<script>
import { VueEditor, Quill } from 'vue2-editor'
import { ImageDrop } from 'quill-image-drop-module'
import ImageUploader from 'quill-image-uploader'
import ImageResize from 'quill-image-resize-module'
import editor from '~/components/editor'

/*
// import Prism Editor
import { PrismEditor } from 'vue-prism-editor'
import 'vue-prism-editor/dist/prismeditor.min.css' // import the styles somewhere
// import highlighting library (you can use any library you want just return html string)
import { highlight, languages } from 'prismjs/components/prism-core'
import 'prismjs/components/prism-clike'
import 'prismjs/components/prism-javascript'
// import 'prismjs/themes/prism-tomorrow.css' // import syntax highlighting styles
// import 'prismjs/components/prism-html'
*/

import htmlX from '~/components/html'

Quill.register('modules/imageDrop', ImageDrop)
Quill.register('modules/imageResize', ImageResize)
Quill.register('modules/imageUploader', ImageUploader)

export default {
  components: {
    htmlX,
    VueEditor,
    editor,
  },
  data() {
    return {
      content: 'kopet is alive',
      editorSettings: {
        modules: {
          imageDrop: true,
          imageResize: {},
          imageUploader: {
            upload: (file) => {
              return new Promise((resolve, reject) => {
                const formData = new FormData()
                formData.append('image', file)
                fetch(
                  'https://api.imgbb.com/1/upload?key=d36eb6591370ae7f9089d85875e56b22',
                  {
                    method: 'POST',
                    body: formData,
                  }
                )
                  .then((response) => response.json())
                  .then((result) => {
                    resolve(result.data.url)
                  })
              })
            },
          },
        },
      },
    }
  },
}
</script>
