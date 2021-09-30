# Django表单

##  表单控件

| 表单字段 | 控件 |
|------|------|
| BooleanField | CheckboxInput |
| CharField | TextInput |
| ChoiceField | Select |
| FilePathField | Select |
| MultipleChoiceField | Select |
| DateField | DateInput |
| DateTimeField | DateInput |
| DecimalField | NumberInput |
| IntegerField | NumberInput |
| FileField | ClearableFileInput |
| ImageField | ClearableFileInput |


## 表单属性

| 表单属性 | 属性说明 |
|------|------|
| required | 表单是否是必填字段 |
| label | 控件对应的label |
| initial | 字段初始值 |
| htlp_text | 控件提示信息 |
| error_messages | 输入错误时的提示信息 |
| localize | 是否启用本地化 |
| disabled | 元素是否disabled |


## 表单使用
```html
<!-- 使用<tr>标签显示表单字段 -->
{{ form.as_table }}

<!-- 使用<p>标签显示表单字段 -->
{{ form.as_p }}

<!-- 使用<li>标签显示表单字段 -->
{{ form.as_ul }}

<!-- 表单隐藏字段 -->
{{ form.hidden_fields }}

<!-- 表单可显示字段 -->
{{ form.as_ul }}
```