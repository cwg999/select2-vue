<template lang="pug">
  .form-group
    label.control-label
      | {{label}}
    select(ref="select" :value="value" @input="reload" @change="reload" name="name")
      slot
</template>
<style scoped lang="scss">
  select {
    width: 100%;
  }
</style>

<script>
export default {
  name:'Select2',
	props: {
    'value':{
      required:true
    },
    'label':{
      type:String
    },
    'options':{
      type:Object,
      required:false
    },
    'name':{
      type:String,
      default:''
    }
  },
	watch: {
		value: function (newVal) {
      console.log(`select2 (${this.name}) value changed - reloading`);
			this.reload(newVal);
		}
	},
	methods:{
    reload : function (value) {
      console.log(`select2 (${this.name}) reload`, value);
      var $select = $(this.$refs.select);
      $select.val(value || this.value).trigger('change');
      console.log('$select.val()',$select.val());
      // $select.select2('destroy');
      // $select.select2(this.options||{});
    }
	},
	mounted: function () {
    console.log(`select2 (${this.name}) mounted`);
    var vm = this;
    var $select = $(this.$refs.select);
    console.log('this.$refs.select',this.$refs.select);
    console.log('select2 mount elem',$select);
		$select.select2(this.options||{});
		$select.val(this.value);
		$select.on('change', function () {
      // console.log(`select2 (${vm.name}) change evt`);
      // console.log(`$select.val()`,$select.val())
      // console.log(`vm.value`,vm.value)
      // console.log(`this.value`,this.value)
      // this.value = $select.val(); // this component cannot set its own prop
      // vm.$emit('input', this.value); // tell the parent to set the new value
      vm.$emit('change', this.value); // tell the parent to set the new value
    });
		$select.on('change.select2', function () {
      // console.log(`select2 (${vm.name}) change.select2 evt`,$select.val(),vm.value);
      // console.log(`$select.val()`,$select.val())
      // console.log(`vm.value`,vm.value)
      // console.log(`this.value`,this.value)
      // this.value = $select.val(); // this component cannot set its own prop
      // vm.$emit('input', this.value); // tell the parent to set the new value
      // vm.$emit('change', this.value); // tell the parent to set the new value
      // console.log(`change.select2 (${vm.name}) val:`,$select.val())
      // vm.$emit('change', vm.value); // tell the parent to set the new value
    });
    $select.trigger('change');
	},
	updated: function () {
    console.log(`select2 (${this.name}) updated`);
    let $select = $(this.$refs.select);
    // $select.trigger('change.select2');
    this.reload(this.value);
	},
	destroyed: function () {
    console.log(`select2 (${this.name}) destroyed`);
    let $select = $(this.$refs.select);
    $select.off('change');
    $select.select2('destroy');
	}
}
</script>