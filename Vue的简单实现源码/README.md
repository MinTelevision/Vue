# 

# proxyData

处理`model`层,数据劫持,把所有的数据绑上一个`set`和`get`
```js
Object.defineProperty(self, key, {
    // 数据一旦变动，我们触发了set的回调，视图就会发生改变
    // 响应数据的改变触发对应的set和get完成对应逻辑
    set(newValue) {
        // 一旦值改变this.$data的值也响应改变
        self.$data[key] = newValue;
        console.log("值发生了更改", newValue)
        // 发布者
        this.$watch.emit(key,null)
    },
    get() {
        console.log("我查看了该值")
        return self.$data[key]
    }
})
```

# 发布订阅者模式

`emit`和`on`

把`proxyData`和`compile`进行一次关联，让视图层和数据层产生关系
```js
let watch = new Observer()
watch.on
watch.emit
```

# compile

编译模板,处理视图层(View)

```
{{name}}  ->  laoyao
```


# 更改数据

经过上面几个不走之后

> proxyData->发布订阅者模式->compile

数据一旦更改，立即触发`set`

触发`set`就会执行发布

compile就会监听，更新视图
```js
vm.name = "lemon"
```