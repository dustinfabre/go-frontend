<template>
  <div>
    <a-row type="flex" justify="center">
      <a-col :span="4">
        <h1><a-icon type="search" /> SEARCH</h1>
      </a-col>
      <a-col :span="16">
        <a-input :model="search" />
      </a-col>
      <a-col :span="20">
        <a-form-item label="Created date">
          <a-input-group compact>
            <a-date-picker style="width: 50%" />
            <a-date-picker style="width: 50%" />
          </a-input-group>
        </a-form-item>
      </a-col>
      <a-col :span="20">
        Total Amount: {{ total }}
      </a-col>
      <a-table
        :columns="columns"
        :row-key="record => record.login.uuid"
        :data-source="data"
        :pagination="pagination"
        :loading="loading"
        @change="handleTableChange"
      />
    </a-row>
  </div>
</template>
<script>
export default {
  data () {
    return {
      search: '',
      total: 0,
      columns: [
        {
          title: 'Order name',
          dataIndex: 'orderName',
          sorter: true,
          width: '20%',
          scopedSlots: { customRender: 'orderName' }
        },
        {
          title: 'Customer Company',
          dataIndex: 'cc'
        },
        {
          title: 'Customer Name',
          dataIndex: 'cn'
        },
        {
          title: 'Order date',
          dataIndex: 'od'
        },
        {
          title: 'Delivered Amount',
          dataIndex: 'da'
        },
        {
          title: 'Total amount',
          dataIndex: 'ta'
        }
      ],
      data: [],
      pagination: {},
      loading: false
    }
  },
  mounted () {
    this.fetch()
  },
  methods: {
    async fetch (params = {}) {
      const ip = await this.$axios.$get('http://localhost:8000/v1/orders')
      console.log(ip)
    },
    handleTableChange () {
      console.log('test')
    }
  }

}
</script>
