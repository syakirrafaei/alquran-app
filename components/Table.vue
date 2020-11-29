<template>
  <div class="flex flex-col my-4">
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div
          class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
        >
          <table class="min-w-full divide-y divide-gray-200">
            <thead>
              <tr>
                <th
                  v-for="th in ths"
                  :key="th.id"
                  scope="col"
                  class="px-6 py-3 bg-gray-200 text-left text-xs font-medium text-gray-900 uppercase tracking-wider"
                >
                  {{ th.value }}
                </th>
              </tr>
            </thead>
            <tbody class="bg-white">
              <tr v-for="(tr, index) in trs" :key="tr.id">
                <td class="px-6 py-2 text-left whitespace-nowrap">
                  <div class="font-medium text-gray-900">
                    {{ index + 1 }}
                  </div>
                </td>
                <td class="px-6 py-2 text-left whitespace-nowrap">
                  <div
                    :class="color.value"
                    class="font-kitab font-medium text-gray-900"
                  >
                    {{ tr.arabic }}
                  </div>
                </td>
                <td class="px-6 py-2 text-left whitespace-nowrap">
                  <div class="font-medium text-gray-900">
                    {{ tr.malay }}
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    ths: null,
    trs: null,
    color: null,
  },
}
</script>
