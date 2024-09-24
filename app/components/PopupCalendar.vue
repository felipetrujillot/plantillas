<script setup lang="ts">
/**
 *
 */
defineProps<{
  title: string
  error?: boolean
}>()

const date = defineModel<string>()

/**
 *
 */
const getStartDate = () => {
  if (date.value === '') return new Date()
  const [dia, mes, anio] = date.value!.split('-')

  const newDat = new Date(
    parseInt(anio!),
    parseInt(mes!) - 1,
    parseInt(dia!),
    0,
    0,
    0,
    0
  )
  return newDat
}

/**
 *
 */
const newDate = computed(() => {
  if (dateCalendar.value) {
    const formattedDate = new Intl.DateTimeFormat('es-CL').format(
      dateCalendar.value
    )
    date.value = formattedDate
    return formattedDate
  }

  date.value = undefined
  return ''
})

const dateCalendar = ref('')
</script>

<template>
  <Popover>
    <PopoverTrigger class="w-full">
      <Card
        class="w-full px-3 py-2 shadow-none flex"
        :class="error ? 'border-warning' : ''"
      >
        <div class="flex items-center gap-1">
          <i class="ph ph-calendar text-xl text-primary-admin"></i>
          <h1 class="text-sm">{{ title }} {{ newDate }}</h1>
        </div>
      </Card>
    </PopoverTrigger>
    <PopoverContent class="p-0">
      <Calendar v-model="dateCalendar" class="rounded-md border" />
    </PopoverContent>
  </Popover>
</template>
