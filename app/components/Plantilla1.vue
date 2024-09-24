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
  <div class="min-h-screen min-w-screen bg-yellow-100" id="screenshot">
    <div class="w-full min-h-screen flex">
      <div class="grid grid-cols-2 w-full min-h-screen">
        <div
          class="border-r border-yellow-600"
          style="border-right-width: 24px"
        >
          <img
            class="min-h-full min-w-full grayscale"
            style="object-fit: cover"
            :src="persona.imagen"
          />
        </div>

        <div class="bg-yellow-50 text-center h-full flex items-center">
          <div
            class="px-20 w-full h-full flex justify-between flex-col py-20 text-yellow-950"
          >
            <div>
              <h1 class="text-3xl" v-html="persona.mensaje_familia"></h1>
            </div>

            <div>
              <div class="flex justify-center">
                <img src="/pigeon-svgrepo-com.svg" class="w-40" />
              </div>
              <h1 class="uppercase tracking-wide text-2xl font-light mt-4">
                {{ persona.nombre_familia }}
              </h1>
            </div>

            <div class="">
              <h1 class="text-4xl">
                {{ persona.nombre }} {{ persona.apellido_paterno }}
                {{ persona.apellido_materno }}
              </h1>

              <h2 class="text-2xl mt-8">
                {{ persona.fecha_nacimiento }} /
                {{ persona.fecha_fallecimiento }}
              </h2>
            </div>
          </div>
          <!-- <TipTap /> -->
        </div>
      </div>
    </div>
  </div>
</template>
