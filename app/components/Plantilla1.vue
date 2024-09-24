<script setup lang="ts">
type Persona = {
  nombre: string
  apellido_paterno: string
  apellido_materno: string
  fecha_nacimiento: string
  fecha_fallecimiento: string
  nombre_familia: string
  mensaje_familia: string
  imagen: string
}

defineProps<{ persona: Persona }>()
</script>
<template>
  <div class="aspect-video" id="screenshot">
    <div class="grid grid-cols-2 h-full">
      <div class="border-r border-yellow-600" style="border-right-width: 24px">
        <img
          :src="persona.imagen"
          style="object-fit: cover"
          class="min-h-full grayscale"
        />
      </div>
      <div class="bg-yellow-50 flex text-center items-center text-yellow-950">
        <div
          class="flex flex-col justify-between h-full md:py-20 py-4 px-8"
          id="real"
        >
          <div>
            <h1
              class="md:text-3xl text-xs"
              v-html="persona.mensaje_familia"
            ></h1>
          </div>

          <div>
            <div class="flex justify-center">
              <img src="/pigeon-svgrepo-com.svg" style="width: 30%" />
            </div>
            <h1
              class="uppercase tracking-wide font-light md:text-2xl text-xs mt-4"
            >
              {{ persona.nombre_familia }}
            </h1>
          </div>

          <div class="">
            <h1 class="font-medium md:text-3xl text-sm">
              {{ persona.nombre }} {{ persona.apellido_paterno }}
              {{ persona.apellido_materno }}
            </h1>

            <h2 class="md:text-2xl text-sm">
              {{ persona.fecha_nacimiento }} /
              {{ persona.fecha_fallecimiento }}
            </h2>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
