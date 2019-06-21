#### React-Magento

A simple way to building HTML forms out of a JSON schema using React Antd UI.

##### 传入 Form 的数据结构

```js
{
  title: 'Todo',
  type: 'object',
  sortdata: ['name', 'description'],
  formOpt: {
    layout: 'horizontal',
    labelCol: { span: 6 },
    wrapperCol: { span: 18 }
  },
  properties: {
    description: {
      type: 'string',
      title: '描述',
      minLength: 30,
      component: 'textarea',
      className: 'test'
    },
    name: {
      type: 'string',
      title: '名字',
      default: 'kico',
      required: true,
      layout: {
        labelCol: { span: 4 },
        wrapperCol: { span: 14, offset: 6 }
      },
    },
    otherinfo: {
      title: '其他信息',
      type: 'object',
      properties: {
        age: { type: 'integer' },
        done: {
          type: 'boolean',
          title: '完成',
          required: true,
          default: false
        },
        county: {
          type: 'string',
          title: '国家',
          enum: ['CN', 'other'],
          enumNames: ['中国', '其他'],
          props: { inline: true }
        }
      }
    }
  }
}
```

##### 使用方式

```js
const Depict = props => {
  const [state, setState] = useState({});

  const changeHandler = source => {
    setState(source.formData);
  };

  const schema = {
    title: 'Todo',
    type: 'object',
    sortdata: ['name', 'description'],
    formOpt: {
      layout: 'horizontal',
      labelCol: { span: 6 },
      wrapperCol: { span: 18 }
    },
    properties: {
      description: {
        type: 'string',
        title: '描述',
        minLength: 30,
        component: 'textarea',
        className: 'test'
      },
      name: {
        type: 'string',
        title: '名字',
        default: 'kico',
        required: true,
        layout: {
          labelCol: { span: 4 },
          wrapperCol: { span: 14, offset: 6 }
        },
      },
      otherinfo: {
        title: '其他信息',
        type: 'object',
        properties: {
          age: { type: 'integer' },
          done: {
            type: 'boolean',
            title: '完成',
            required: true,
            default: false
          },
          county: {
            type: 'string',
            title: '国家',
            enum: ['CN', 'other'],
            enumNames: ['中国', '其他'],
            props: { inline: true }
          }
        }
      }
    }
  };

  return (
    <AntdForm
      schema={schema}
      formData={state}
      onChange={changeHandler}
      onSubmit={log('submitted')}
      onError={log('errors')}
    />
  );
}
```

##### Form 返回的字段

```js
{
  name: "kico",
  description: "test",
  otherinfo: {
    age: 17,
    done: true,
    county: 'CN'
  }
}
```

##### 自定义 Api

|字段|描述|类型|
|----|---|---|
|sortdata|字段排序| array |
|formOpt|antd 表单的布局| object |
|required|字段是否必须|boolean|
|layout|Form.Item 的布局 |object|
|component|字段的展现形式|-|
|className|字段的样式|string|
|props|字段的其他特殊限制|object|
|condition|字段的关联条件|string|
|option|字段的配置|object|
|validate|自定义字段校验|-|
|format|自定义字段格式化|-|

