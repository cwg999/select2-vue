Possible usage:

(Pug/Jade)
```pug
    Select2(
      :value="inputs.thing" 
      @input="inputs.thing = arguments[0]"
      @change="inputs.thing = arguments[0]"
      label="Thing"
      name="thing-input"
    )
      option(v-for="l,key in this.things" :key="key" :value="key") {{l.name}}
```
(HTML)
```html
    <Select2 
      :value="inputs.thing" 
      @input="inputs.thing = arguments[0]"
      @change="inputs.thing = arguments[0]"
      label="Thing"
      name="thing-input"
    >
      <option v-for="l,key in this.things" :key="key" :value="key">
        {{l.name}}
      </option>
    </Select2>
```