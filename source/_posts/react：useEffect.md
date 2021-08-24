---
title: 'react: useEffect'
date: 2020-10-27 19:46:05
tags: react
category: 阅读笔记
---
本文是在学习[useEffect完整指南](https://overreacted.io/zh-hans/a-complete-guide-to-useeffect/)中做的笔记，记录自己不理解的地方以及学到的知识。

### 🍀 每一次渲染都有它自己的Props和State

### 🍀 每一次渲染都有它自己的事件处理函数

<!--more-->

### 🍀 每一次渲染都有它自己的Effects

每一个组件内的函数（包括事件处理函数，effects，定时器或者API调用等等）都会捕捉某次渲染中定义的props和state。

React会根据我们当前的props和state同步到DOM。

useEffect使你能够根据props和state同步React tree之外的东西。

useEffect中的依赖项用来告诉React去对比你的Effects。

### 🍀 关于依赖项不要对React撒谎

* 诚实告知依赖

  * 在依赖中包含所有effect中用到的组件内的值。

  * 修改effect内部的代码，以确保它包含的值只会在需要的时候发生变更。

### 🍀 函数式更新

```
useEffect(() => {
    const id = setInterval(() => {
      setCount(c => c + 1);
    }, 1000);
    return () => clearInterval(id);
  }, []);
```

例如用`setCount(c => c + 1)` 代替  `setCount(count+1)`, 在effect中传递最小的信息

### 🍀 解耦来自Actions的更新

```
function Counter() {
  const [count, setCount] = useState(0);
  const [step, setStep] = useState(1);

  useEffect(() => {
    const id = setInterval(() => {
      setCount(c => c + step);
    }, 1000);
    return () => clearInterval(id);
  }, [step]);

  return (
    <>
      <h1>{count}</h1>
      <input value={step} onChange={e => setStep(Number(e.target.value))} />
    </>
  );
}
```

当你想更新一个状态，并且这个状态更新依赖于另一个状态的值时，你可能需要使用`useReducer`去替换它们。

```
const [state, dispatch] = useReducer(reducer, initialState);
const { count, step } = state;

useEffect(() => {
  const id = setInterval(() => {
    dispatch({ type: 'tick' }); // Instead of setCount(c => c + step);
  }, 1000);
  return () => clearInterval(id);
}, [dispatch]);
```

React会保证`dispatch`在组件的生命周期内保持不变。