<script setup lang="ts">
import { toPng } from 'html-to-image'

useHead({
  title: `Plantillas`,
  meta: [{ name: 'description', content: 'plantillas' }],
})

const persona = ref({
  nombre: '',
  apellido_paterno: '',
  apellido_materno: '',
  fecha_nacimiento: '01-01-2000',
  fecha_fallecimiento: '',
  nombre_familia: '',
  mensaje_familia: '',
  imagen: '',
})
/**
 *
 * @returns
 */
const getFormattedDate = () => {
  const date = new Date()

  const year = date.getFullYear()
  const month = String(date.getMonth() + 1).padStart(2, '0') // getMonth() returns 0-11
  const day = String(date.getDate()).padStart(2, '0')
  const hours = String(date.getHours()).padStart(2, '0')
  const minutes = String(date.getMinutes()).padStart(2, '0')
  const seconds = String(date.getSeconds()).padStart(2, '0')

  return `${year}${month}${day}${hours}${minutes}${seconds}`
}

const downloadScreenshot = async () => {
  const date = getFormattedDate()
  const width = window.innerWidth
  const real = document.getElementById('real')!
  const height = real.offsetHeight

  const screenshot = document.getElementById('screenshot')!

  const dataUrl = await toPng(screenshot, {
    width: width,
    height: height,
    canvasHeight: height,
    canvasWidth: width,
  })

  let link = document.createElement('a')
  link.download = `${date}.png`
  link.href = dataUrl
  link.click()
}

const view = ref<'form' | 'plantilla_1'>('form')

const docHandler = ($event: Event) => {
  const target = $event.target as HTMLInputElement
  if (target && target.files) {
    const file = target.files[0]
    persona.value.imagen = URL.createObjectURL(file!)
  }
}
</script>

<template>
  <div class="fixed z-10 flex justify-center bottom-0 w-full items-end">
    <div class="flex gap-4 py-4">
      <Button :disabled="view === 'form'" @click.prevent="view = 'form'">
        Volver
      </Button>
      <Button :disabled="view === 'form'" @click.prevent="downloadScreenshot"
        >Descargar</Button
      >
      <Button @click.prevent="view = 'plantilla_1'">Siguiente</Button>
    </div>
  </div>
  <div
    v-if="view === 'form'"
    class="flex min-w-screen min-h-screen bg-neutral-100"
  >
    <div class="container-sm w-full h-full my-16 px-2">
      <Card class="space-y-4">
        <h1 class="text-2xl font-bold">Datos personales</h1>
        <div class="space-y-1">
          <Label>Nombre</Label>
          <Input v-model="persona.nombre" placeholder="Ej: Juan" />
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div class="space-y-1">
            <Label>Apellido Paterno</Label>
            <Input
              v-model="persona.apellido_paterno"
              placeholder="Ej: Martinez"
            />
          </div>
          <div class="space-y-1">
            <Label>Apellido Materno</Label>
            <Input v-model="persona.apellido_materno" placeholder="Ej: Perez" />
          </div>
        </div>

        <div>
          <Label>Nombre Familia</Label>
          <Input
            v-model="persona.nombre_familia"
            placeholder="Ej: Familia Perez"
          />
        </div>

        <div>
          <Label>Mensaje Familia</Label>
          <TipTap v-model="persona.mensaje_familia" />
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div>
            <Label>Fecha Nacimiento</Label>
            <PopupCalendar v-model="persona.fecha_nacimiento" title="Fecha:" />
          </div>

          <div>
            <Label>Fecha Fallecimiento</Label>
            <PopupCalendar
              v-model="persona.fecha_fallecimiento"
              title="Fecha:"
            />
          </div>
        </div>

        <div>
          <Label>Imagen</Label>

          <Input
            type="file"
            ref="documentUpload"
            @change="docHandler"
            accept="image/*"
            capture
          />

          <img
            class="w-20 h-20 mt-4"
            :src="persona.imagen"
            v-if="persona.imagen.length > 1"
          />
        </div>
      </Card>
    </div>
  </div>
  <Plantilla1 v-if="view === 'plantilla_1'" :persona="persona" />
</template>

<style>
.grayscale {
  -webkit-filter: grayscale(100%);
  filter: grayscale(100%);
}
.container-sm {
  width: 100%;
  margin-right: auto;
  margin-left: auto;
  max-width: 960px;
}
</style>
