### vue的构造函数开始：
1. src.core.instance.index 实例化入口
```JavaScript
function Vue (options) {
  // 判断实例化语法是否合法，之后在调用初始化方法
  if (process.env.NODE_ENV !== 'production' && !(this instanceof Vue)) {
    warn('Vue is a constructor and should be called with the `new` keyword')
  }
  this._init(options)
}

initMixin(Vue)
stateMixin(Vue)
eventsMixin(Vue)
lifecycleMixin(Vue)
renderMixin(Vue)
```

2. src.core.instance.init中的_init()方法
```JavaScript
Vue.prototype._init = function (options?: Object) {
    const vm: Component = this
    // a uid
    vm._uid = uid++ // 实例的唯一标示uid累加

    let startTag, endTag
    /* istanbul ignore if */ // 此处的注释，意思是Istanbul代码覆盖率计算的时候，忽略下面的if中的代码
    // if中与性能统计有关
    if (process.env.NODE_ENV !== 'production' && config.performance && mark) {
      startTag = `vue-perf-start:${vm._uid}`
      endTag = `vue-perf-end:${vm._uid}`
      mark(startTag)
    }

    // a flag to avoid this being observed
    vm._isVue = true // 监听对象变化时忽略vm
    // merge options
    if (options && options._isComponent) { // 当内部创建子组件时，_isComponent为true，才会进行下面条件
      // optimize internal component instantiation
      // since dynamic options merging is pretty slow, and none of the
      // internal component options needs special treatment.
      initInternalComponent(vm, options)
    } else {
      vm.$options = mergeOptions( 
        // vue中使用的一个用来合并对象的方法，不过和Object.assign等相比，vue会在期间进行一些操作
        resolveConstructorOptions(vm.constructor),
        options || {},
        vm
      )
    }
    /* istanbul ignore else */
    if (process.env.NODE_ENV !== 'production') {
      /*      */
      initProxy(vm)
    } else {
      vm._renderProxy = vm
    }
    // expose real self 对外暴露自身,即进行接下来实例化各个属性等操作
    vm._self = vm
    initLifecycle(vm)
    initEvents(vm)
    initRender(vm)
    callHook(vm, 'beforeCreate')
    initInjections(vm) // resolve injections before data/props
    initState(vm)
    initProvide(vm) // resolve provide after data/props
    callHook(vm, 'created')

    /* istanbul ignore if */ // 同开始的性能
    if (process.env.NODE_ENV !== 'production' && config.performance && mark) {
      vm._name = formatComponentName(vm, false)
      mark(endTag)
      measure(`vue ${vm._name} init`, startTag, endTag)
    }

    if (vm.$options.el) {
      vm.$mount(vm.$options.el)
    }
  }
```

在上段代码中，vue初始化会调用resolveConstructorOptions方法来生成vm.$options，下面是该方法：
```JavaScript
export function resolveConstructorOptions (Ctor: Class<Component>) {
  let options = Ctor.options
  if (Ctor.super) { // 是否有super属性，一般使用Vue.extend()方法会有super
    const superOptions = resolveConstructorOptions(Ctor.super)
    // 返回值父类的options
    const cachedSuperOptions = Ctor.superOptions
    // 自身的options
    if (superOptions !== cachedSuperOptions) {
      // 若发生了变化，说明父类的options进行了改变，此时需要更新自身的options到最新值
      // super option changed,
      // need to resolve new options.
      Ctor.superOptions = superOptions
      // check if there are any late-modified/attached options (#4976)
      const modifiedOptions = resolveModifiedOptions(Ctor)
      // 之后检查自身的options是否发生了变化，resolveModifiedOptions下面记录
      // update base extend options
      if (modifiedOptions) {
        extend(Ctor.extendOptions, modifiedOptions)
      }
      options = Ctor.options = mergeOptions(superOptions, Ctor.extendOptions)
      if (options.name) {
        options.components[options.name] = Ctor
      }
    }
  }
  return options
}
```
```javascript
// 整理变化的options并返回
function resolveModifiedOptions (Ctor: Class<Component>): ?Object {
  let modified
  const latest = Ctor.options // 自身options
  const extended = Ctor.extendOptions // 构造器传入的options
  const sealed = Ctor.sealedOptions // 执行Vue.extend时封装的"自身"options，记录并用来比较自身options有无变化
  for (const key in latest) {
    if (latest[key] !== sealed[key]) { // 不存在或者值不同，考虑数组情况
      if (!modified) modified = {}
      modified[key] = dedupe(latest[key], extended[key], sealed[key])
      // 执行该方法后，讲新的options存在modified中，具体逻辑如下
    }
  }
  return modified
}

// 遍历新增或者不同的options值，并将新值或者变化数组中新增的值整理为数组返回
function dedupe (latest, extended, sealed) {
  // lateset表示的是自身新增的options。
  // extended表示的是当前构造器上新增的options
  // sealed表示的是当前构造器上新增的封装options。
  
  // compare latest and sealed to ensure lifecycle hooks won't be duplicated
  // between merges
  if (Array.isArray(latest)) {
    const res = []
    sealed = Array.isArray(sealed) ? sealed : [sealed]
    extended = Array.isArray(extended) ? extended : [extended]
    for (let i = 0; i < latest.length; i++) {
      // push original options and not sealed options to exclude duplicated options
      if (extended.indexOf(latest[i]) >= 0 || sealed.indexOf(latest[i]) < 0) {
        res.push(latest[i])
      }
    }
    return res
  } else {
    return latest
  }const modifiedOptions = resolveModifiedOptions(Ctor)
      // 之后检查自身的options是否发生了变化，resolveModifiedOptions下面记录
      // update base extend options
      if (modifiedOptions) {
        extend(Ctor.extendOptions, modifiedOptions)
      }
      options = Ctor.options = mergeOptions(superOptions, Ctor.extendOptions)
      if (options.name) {
        options.components[options.name] = Ctor
      }
}

```
大致了解之后，回到resolveConstructorOptions方法，此时
const modifiedOptions = resolveModifiedOptions(Ctor)
这一行代码的执行结果已经返回了。
```JavaScript
if (modifiedOptions) { // 把新添加的options属性添加到Ctor.extendOptions属性上
   extend(Ctor.extendOptions, modifiedOptions)
}
options = Ctor.options = mergeOptions(superOptions, Ctor.extendOptions)
// 调用mergeOptions方法合并父类构造器上的options和自身上的extendOptions
if (options.name) {
  options.components[options.name] = Ctor
}
```
