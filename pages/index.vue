<template>
  <div>
    <style rel="stylesheet" type="text/css" href="https://cdn3.devexpress.com/jslib/22.2.6/css/dx.light.css" />
    <LineChar
      id='my-chart-id'
      :chart-options='options'
      :chart-data='data'
      style='height: 300px'
    />
    <DxDataGrid
      id='gridContainer'
      :data-source='dataSource'
      :show-borders='true'
      :selected-row-keys='selectedItemKeys'
      @selection-changed='selectionChanged'
    >
      <DxEditing
        :allow-updating='true'
        :allow-adding='true'
        :allow-deleting='true'
        mode='cell'
      />
      <DxPaging :enabled='false' />
      <DxSelection mode='multiple' />
      <DxColumn
        :width='55'
        data-field='Prefix'
        caption='Title'
      />
      <DxColumn
        data-field='FirstName'
      />
      <DxColumn
        data-field='LastName'
      />
      <DxColumn
        :width='170'
        data-field='Position'
      />
      <DxColumn
        :width='125'
        data-field='StateID'
        caption='State'
      >
        <DxLookup
          :data-source='states'
          value-expr='ID'
          display-expr='Name'
        />
      </DxColumn>
      <DxColumn
        data-field='BirthDate'
        data-type='date'
      />
      <DxToolbar>
        <DxItem
          name='addRowButton'
          show-text='always'
        />
        <DxItem location='after'>
          <template #default>
            <DxButton
              @click='deleteRecords()'
              :disabled='!selectedItemKeys.length'
              icon='trash'
              text='Delete Selected Records'
            />
          </template>
        </DxItem>
      </DxToolbar>
    </DxDataGrid>
  </div>

</template>

<script>
import {
  DxDataGrid,
  DxColumn,
  DxPaging,
  DxEditing,
  DxSelection,
  DxLookup,
  DxToolbar,
  DxItem,
  DxButton
} from 'devextreme-vue/data-grid'
import { Line as LineChar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  PointElement,
  LineElement,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'


import DataSource from 'devextreme/data/data_source'
import ArrayStore from 'devextreme/data/array_store'

import { employees, states } from '~/assets/data.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, PointElement, LineElement)

export default {
  name: 'BarChart',
  components: {
    LineChar,
    DxDataGrid,
    DxColumn,
    DxPaging,
    DxEditing,
    DxSelection,
    DxLookup,
    DxButton,
    DxToolbar,
    DxItem
  },
  data() {
    return {
      chartData: {
        labels: ['1', '2', '3'],
        datasets: [{ data: [40, 20, 12] }]
      },
      chartOptions: {
        responsive: true
      },
      options: {
        responsive: true,
        maintainAspectRatio: false
      },
      data: {
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            yAxes: [{
              ticks: {
                beginAtZero: true
              }
            }]
          }
        },

        labels: ['1', '2', '3', '4', '5', '6', '7'],
        datasets: [
          {
            label: 'Data One',
            borderColor: 'rgba(75, 192, 192, 1)',
            backgroundColor: 'rgba(75, 192, 192, 0.2)',
            data: [40, 39, 10, 40, 39, 80, 40]
          },
          {
            label: 'Data two',
            borderColor: 'rgba(192, 192, 192, 1)',
            backgroundColor: 'rgba(192, 192, 192, 0.2)',
            data: [140, 139, -10, -40, 39, 80, 40]
          }
        ]

      },
      dataSource: new DataSource({
        store: new ArrayStore({
          data: employees,
          key: 'ID'
        })
      }),
      selectedItemKeys: [],
      states,
      selectionChanged: (data) => {
        this.selectedItemKeys = data.selectedRowKeys
      },
      deleteRecords: () => {
        this.selectedItemKeys.forEach((key) => {
          this.dataSource.store().remove(key)
        })
        this.selectedItemKeys = []
        this.dataSource.reload()
      }
    }
  }
}
</script>
<style>
#data-grid-demo {
  min-height: 700px;
}

#gridDeleteSelected {
  position: absolute;
  z-index: 1;
  right: 0;
  margin: 1px;
  top: 0;
}

#gridDeleteSelected .dx-button-text {
  line-height: 0;
}
</style>
