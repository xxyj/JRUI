---
title: 下拉选择
is_beta: true
---

## 代码演示

### 基本形式

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-select source={source} lang="en-US" />
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        source: [
            {name: '选项1'},
            {name: '选项2'},
            {name: '选项3'}
        ]
    }
});
```
<!-- demo_end -->

### 表单项

在表单中使用

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-form>
    <jr-form-item cols="12" title="用户名" hint="用户名的用途">
        <jr-select source={['简单选项1', '简单选项2', '简单选项3']} />
    </jr-form-item>
</jr-form>
```
<!-- demo_end -->

### selected, value和key

`selected`表示当前选择项，`value`表示当前选择值。`key`表示数据项的键，默认为`'id'`。

它们三者的关系如下：`selected[key] == value`。其中`selected`和`value`是联动的，当一项变化时会同时改变另一项。

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-form>
    <jr-form-item cols=4>
        <jr-select source={source} selected={selected} />
    </jr-form-item>
    <jr-form-item cols=4>
        <jr-select source={source} value=2 />
    </jr-form-item>
    <jr-form-item cols=4>
        <jr-select source={source} key="name" value="选项3" />
    </jr-form-item>
</jr-form>
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        source: [
            {id: 1, name: '选项1'},
            {id: 2, name: '选项2'},
            {id: 3, name: '选项3'}
        ]
    },
    config: function() {
        this.data.selected = this.data.source[0];
    }
});
```
<!-- demo_end -->

### 禁用某一项，禁用组件
`tip`表示禁用某一项时给出的提示，不给则无提示，`placement`表示给出提示的方向，具体参考文字提示组件Tooltip

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-form>
    <jr-form-item cols=6>
        <jr-select source={source} />
    </jr-form-item>
    <jr-form-item cols=6>
        <jr-select source={source} disabled />
    </jr-form-item>
</jr-form>
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        source: [
            {name: '选项1'},
            {name: '选项2'},
            {name: '选项3（禁用）', disabled: true},
            {name: '选项4（禁用）', disabled: true, tip: 'tip'},
            {name: '选项5（禁用）', disabled: true, tip: 'tip', placement: 'bottom'}
        ]
    }
});
```
<!-- demo_end -->

### 分隔线

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-form>
    <jr-form-item cols=12>
        <jr-select source={source} />
    </jr-form-item>
</jr-form>
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        source: [
            {name: '选项1'},
            {name: '选项2'},
            {divider: true},
            {name: '选项3（禁用）', disabled: true}
        ]
    }
});
```
<!-- demo_end -->

### 设置或取消默认项

如果`placeholder`为空，刚开始将会自动选中第一项。

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-form>
    <jr-form-item cols=6>
        <jr-select source={source} placeholder="全部" />
    </jr-form-item>
    <jr-form-item cols=6>
        <jr-select source={source} placeholder="" />
    </jr-form-item>
</jr-form>
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        source: [
            {name: '选项1'},
            {name: '选项2'},
            {name: '选项3'}
        ]
    }
});
```
<!-- demo_end -->

### 远程数据

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-select service={@(this.service)} value="2" />
```

```javascript
var component = new JRUI.Component({
    template: template,
    service: {
        key:'searchValue',
        getList: function(params, success) {
            this.$update('source', ['a','adv','3ds','erd','ssa','ddf','dd','d','33d','10','11'].filter(item=>{
                         return item.indexOf(params.searchValue)!==-1
                     }));
        }
    }
});
```
<!-- demo_end -->

### 数据绑定

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-select source={source} selected={selected} value={value} /> 当前选择项：{selected ? selected.name : 'undefined'}，当前选择值：{value || 'undefined'}
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        source: [
            {id: 1, name: '选项1'},
            {id: 2, name: '选项2'},
            {id: 3, name: '选项3'}
        ]
    }
});
```
<!-- demo_end -->

### 事件

请打开浏览器的控制台查看结果。

<!-- demo_start -->
<div class="m-example"></div>

```xml
<jr-select source={source}
    on-toggle={console.log('on-toggle:', '$event.open:', $event.open)}
    on-select={console.log('on-select:', '$event.selected:', $event.selected)}
    on-change={console.log('on-change:', '$event:', $event)} />
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        source: [
            {name: '选项1'},
            {name: '选项2'},
            {name: '选项3'}
        ]
    }
});
```
<!-- demo_end -->

### 综合示例

<!-- demo_start -->
<div class="m-example"></div>

```xml
<div class=g-row>
    <jr-button title="是否多选" on-click={this.toggleMultiple(multiple)}/>
    {multiple?'true:可多选':'false:不可多选'}
</div>
<div class=g-row>
    <jr-button title="是否有全选" on-click={this.toggleCanSelectAll(canSelectAll)}/>
    {canSelectAll?'true:有':'false:无'}
</div>
<div class=g-row>
    <jr-button title="是否选中关闭" on-click={this.toggleSelectedClose(selectedClose)}/>
    {canSelectAll?'true:有':'false:无'}
</div>
<div class=g-row>
    展示字段分隔符：
    <jr-input value={showSeparator}/>
    value分隔符：
    <jr-input value={separator}/>
</div>
<div class=g-row>
    最多展示多少个选项：
    <jr-input value={limit}/>
</div>
<div class=g-row>
    <jr-button title="是否可搜索" on-click={this.toggleCanSearch(canSearch)}/>
    {canSearch?'true:可搜索':'false:不可搜索'}
</div>
<div class=g-row>
    <jr-button title="区分大小写" on-click={this.toggleSensitive(isCaseSensitive)}/>
    {isCaseSensitive?'true:区分大小写':'false:不区分大小写'}
</div>
<jr-select source={source} multiple={multiple} canSearch={canSearch}
            showSeparator={showSeparator} separator={separator}
            selectedClose={selectedClose} canSelectAll={canSelectAll}
            isCaseSensitive={isCaseSensitive} searchInputPlaceholder="请输入"
            value={value} limit={limit}/>
<div class=g-row>
    选中值：{value}
</div>
```

```javascript
var component = new JRUI.Component({
    template: template,
    data: {
        multiple: true,
        separator: ',',
        showSeparator: '、',
        selectedClose: false,
        canSelectAll: true,
        canSearch: true,
        isCaseSensitive: false,
        value: '',
        limit: null,
        source: [
            {name: '选项A'},{name: '选项a'},{name: '选项B'},{name: '选项b'},{name: '选项C'},{name: '选项c'},
            {name: '选项D'},{name: '选项d'},{name: '选项E'},{name: '选项e'},{name: '选项F'},{name: '选项f'},
            {name: '选项G'},{name: '选项g'},{name: '选项H'},{name: '选项h'},{name: '选项I'},{name: '选项i'},
            {name: '选项J'},{name: '选项j'},{name: '选项K'},{name: '选项k'},{name: '选项L'},{name: '选项l'},
            {name: '选项M'},{name: '选项m'},{name: '选项N'},{name: '选项n'},{name: '选项O'},{name: '选项o'},
            {name: '选项P'},{name: '选项p'},{name: '选项Q'},{name: '选项q'},{name: '选项R'},{name: '选项r'},
            {name: '选项S'},{name: '选项s'},{name: '选项T'},{name: '选项t'},{name: '选项U'},{name: '选项u'},
            {name: '选项V'},{name: '选项v'},{name: '选项W'},{name: '选项w'},{name: '选项X'},{name: '选项x'},
            {name: '选项Y'},{name: '选项y'},{name: '选项Z'}
        ]
    },
    toggleSelectedClose: function(selectedClose){
        this.data.selectedClose = !selectedClose;
    },
    toggleCanSelectAll: function(canSelectAll){
        this.data.canSelectAll = !canSelectAll;
    },
    toggleMultiple: function(multiple){
        this.data.multiple = !multiple;
    },
    toggleCanSearch: function(CanSearch){
        this.data.canSearch = !CanSearch;
    },
    toggleSensitive: function(isCaseSensitive){
        this.data.isCaseSensitive = !isCaseSensitive;
    }
});
```
<!-- demo_end -->
