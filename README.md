# vue-simpleui-mobile
一个适用于移动端的简单vue组件，用来学习vue练手的，目前只添加了日历组件和选择日历范围组件。
### 安装
```
npm run vue-simpleui-mobile
```

## 安装项目依赖
```
npm install
```

### 运行示例
```
npm run serve
```

### 测试
```
npm run test:unit
```

### 测试覆盖率

### API
#### Calendar
| 参数 | 说明 | 类型 | 返回 | 默认值 |
|---|---|---|---|---|
|defaultValue | 默认日期 | string | null | - |
|onChange | 点确定按钮时的事件回调 | function | array |'' |

#### RangeCalendar
| 参数 | 说明 | 类型  | 返回 | 默认值 |
|---|---|---|---|---|
|rangeValue | 默认时间日期范围 | array | null | - |
|onChange | 点确定按钮时的事件回调 | function | array | null |