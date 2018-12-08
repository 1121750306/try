```JavaScript
// 合并构造函数原本的options和构造时传入的options
export function mergeOptions (
  parent: Object, // 构造函数上的options
  child: Object, // 构造时传入的options
  vm?: Component // 实例化本身
): Object {
  if (process.env.NODE_ENV !== 'production') {
    checkComponents(child) // 方法内容见下文
    // 检查组件名是否合法
  }

  if (typeof child === 'function') {
    child = child.options
  }

  normalizeProps(child, vm)
  normalizeInject(child, vm)
  normalizeDirectives(child)
  // 这三个方法的作用类似，都是讲props，inject，directives属性转为对象的形式，例如有时候会传入数组的形似：
  // Vue.component('blog-post', {
  //    props: ['postTitle'],
  //    template: '<h3>{{ postTitle }}</h3>'
  // })
  
  const extendsFrom = child.extends
  if (extendsFrom) {
    parent = mergeOptions(parent, extendsFrom, vm)
  }
  // 上下部分代码：子options如果有mixins或者extends，则需要重新调用mergeOptions来合并这些属性
  if (child.mixins) {
    for (let i = 0, l = child.mixins.length; i < l; i++) {
      parent = mergeOptions(parent, child.mixins[i], vm)
    }
  }
  const options = {}
  let key
  for (key in parent) {
    mergeField(key)
  }
  for (key in child) {
    if (!hasOwn(parent, key)) {
      mergeField(key)
    }
  }
  function mergeField (key) {
    const strat = strats[key] || defaultStrat
    options[key] = strat(parent[key], child[key], vm, key)
  }
  // defaultStrat 默认合并策略， 子没有就取父的，子有就取子的
  /*const defaultStrat = function (parentVal: any, childVal: any): any {
    return childVal === undefined
      ? parentVal
      : childVal
  }*/
```

检查构造时传入的options中，components中引入的组件名是否合法
```JavaScript
function checkComponents (options: Object) {
  for (const key in options.components) {
    // 遍历传入options中的components，并验证引入的组件的合法性
    validateComponentName(key)
  }
}

export function validateComponentName (name: string) {
  if (!/^[a-zA-Z][\w-]*$/.test(name)) { // 命名是否符合正则中的规则
    warn(
      'Invalid component name: "' + name + '". Component names ' +
      'can only contain alphanumeric characters and the hyphen, ' +
      'and must start with a letter.'
    )
  }
  if (isBuiltInTag(name) || config.isReservedTag(name)) {
    // isBuiltInTag方法是检验该名是否与svg标签或者html标签相同
    // isReservedTag方法，检验是否和保留字相同
    warn(
      'Do not use built-in or reserved HTML elements as component ' +
      'id: ' + name
    )
  }
}
```
下面是讲props统一处理为对象形式的方法，inject和directive具体思路类似，区别在于各自特有的小部分
```JavaScript
function normalizeProps (options: Object, vm: ?Component) {
  const props = options.props
  if (!props) return
  const res = {}
  let i, val, name
  if (Array.isArray(props)) {
    i = props.length
    while (i--) {
      val = props[i]
      if (typeof val === 'string') {
        name = camelize(val) // 短横线转驼峰
        res[name] = { type: null }
      } else if (process.env.NODE_ENV !== 'production') {
        warn('props must be strings when using array syntax.')
      }
    }
  } else if (isPlainObject(props)) { 
    // 验证是否是对象，isPlainObject内部调用的是Object.prototype.tostring.call()和[object Object]字符串进行对比
    for (const key in props) {
      val = props[key]
      name = camelize(key)
      if (process.env.NODE_ENV !== 'production' && isPlainObject(val)) {
        validatePropObject(name, val, vm) 
        
        /* const propOptionsRE = /^(type|default|required|validator)$/
        校验prop对象中，类似type或者required等是否正确合法
        function validatePropObject (
          propName: string,
          prop: Object,
          vm: ?Component
        ) {
          for (const key in prop) {
            if (!propOptionsRE.test(key)) {
              warn(
                `Invalid key "${key}" in validation rules object for prop "${propName}".`,
                vm
              )
            }
          }
        }*/
        
      }
      res[name] = isPlainObject(val)
        ? val
        : { type: val }
    }
  } else if (process.env.NODE_ENV !== 'production') {
    warn(
      `Invalid value for option "props": expected an Array or an Object, ` +
      `but got ${toRawType(props)}.`,
      vm
    )
  }
  options.props = res
}
```





其他合并策略
