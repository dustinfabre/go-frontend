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
          dataIndex: 'order_name',
          sorter: true,
          width: '20%',
          scopedSlots: { customRender: 'orderName' }
        },
        {
          title: 'Customer Company',
          dataIndex: 'customer_company'
        },
        {
          title: 'Customer Name',
          dataIndex: 'customer_name'
        },
        {
          title: 'Order date',
          dataIndex: 'order_date'
        },
        {
          title: 'Delivered Amount',
          dataIndex: 'delivered_amount'
        },
        {
          title: 'Total amount',
          dataIndex: 'total_amount'
        }
      ],
      data: [],
      pagination: {},
      loading: false,
      start: 0,
      end: 5
    }
  },
  mounted () {
    this.fetch()
  },
  methods: {
    async fetch (params = {}) {
      const ip = await this.$axios.$post('http://localhost:8000/v1/orders', {
        start: this.start,
        end: this.end
      })
      this.data = ip
      console.log(ip)
    },
    handleTableChange () {
      console.log('test')
    }
  }

}
</script>
