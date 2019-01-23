## So, what in the world is MVC?



### Дорогой интернет, что такое MVC?

<div>
    <img src="img/imvc1.png" width="20%" />
    <img src="img/imvc2.png" width="33%" />
    <img src="img/imvc3.png" width="33%" />
</div>
<div>
    <img src="img/imvc4.png" width="33%" />
    <img src="img/imvc5.png" width="33%" />
</div>
<img src="img/imvc6.png" style="position: absolute; width: 33%; top: 50%; left: 50%; transform: translate(-50%, -50%);" />



### И это не все!

<img src="img/mv-star-2.jpg" />



### Какая схема правильная/наилучшая?

#### Да они все ничего.
<blockquote>
<p>MVC часто называют паттерном, но я не вижу особой пользы воспринимать его как паттерн,
поскольку он включает в себя множество различных идей.</p>
<p>Разные люди читают про MVC в различных источниках и извлекают оттуда разные идеи, но называют их одинаково — «MVC».
Это приводит к большой путанице и кроме того служит источником недоразумений и непониманию MVC,
как будто бы люди узнавали про него через «испорченный телефон»…</p>
<p>Я уже потерял счет сколько раз я видел что-то, описываемое как MVC, которое им не оказывалось.</p>
<footer>&nbsp; ― &nbsp;Мартин Фаулер</footer>
</blockquote>



### Приложение без архитектуры
<img src="/img/spaghetti.jpg" />



### Шаг 1. Divide and Conquer

<img src="img/mvc-step-1.png" />



### Шаг 2. Low Coupling

<div class="flex">
<pre style="width: 57%"><code class="javascript" data-trim data-noescape>
class TodoModel {
  constructor(view) {
    this.view = view;
    this.list = [
      { title: "Wake up", completed: false }
      { title: "Cloud dispersal", completed: false }
    ];
  }

  getTodos() {
    return this.list;
  }

  setCompleted(id) {
    this.list[id].completed = true;
    this.view.notify();
  }
}
</code></pre>
<pre style="width: 42%"><code class="javascript" data-trim data-noescape>
class TodoUI {
  constructor(model) {
    this.model = model;
  }

  notify() {
    this.render();
  }

  render(data) {
    const data = this.model.getTodos();
    . . .
  }
}
</code></pre>
</div>



### `Observer`

<div class="flex">
<pre style="width: 57%"><code class="javascript" data-trim data-noescape>
class TodoModel {
  constructor() {
<mark>&nbsp;</mark>   this.observer = new Observable();
    this.list = [
      { title: "Wake up", completed: false }
      { title: "Cloud dispersal", completed: false }
    ];
  }

  getTodos() {
    return this.list;
  }

  setCompleted(id) {
    this.list[id].completed = true;
<mark>&nbsp;</mark>   this.observer.notify();
  }

<mark>&nbsp;</mark> subscribe(cb) {
<mark>&nbsp;</mark>   this.observer.subscribe(cb);
<mark>&nbsp;</mark> }
}
</code></pre>
<pre style="width: 42%"><code class="javascript" data-trim data-noescape>
class TodoUI {
  constructor(model) {
    this.model = model;
<mark>&nbsp;</mark>   this.model.subscribe(
<mark>&nbsp;</mark>     this.notify.bind(this));
  }

  notify() {
    this.render(data);
  }

  render(data) {
    const data = this.model.getTodos();
    . . .
  }
}
</code></pre>
</div>



### Шаг 3. Low Coupling-2

<img src="img/even-lower.jpg" />



### Façade

<div class="flex">
  <div style="width: 70%">
    <img src="img/facade-diagram.png" />
  </div>
  <div>
    <img src="img/facade-old.png" />
  </div>
</div>



### Шаг 4: Divide and Conquer-2

<img src="img/mvc-step-2.png" />



### Who are you, Mr. Controller?

<div class="flex">
  <img src="img/old-view-editor-1.png" style="height: 80%" />
  <div><img src="img/old-view-editor-2.png" /></div>
</div>



### Схемы MVC
<div class="flex">
  <div>
    <img src="img/mvc-1.png" />
  </div>
  <div>
    <img src="img/mvc-2.png" />
  </div>
</div>



### Facebook и все-все-все
<div class="fragment">фатальный недостаток: MVC написали не мы!</div>

<div class="flex">
    <div>
        <img src="img/why-not-mvc.png" class="fragment" />
    </div>
    <div class="fragment">
        <img src="img/flux.png" class="fragment fade-out"  />
        <img src="img/flux-reality.png" class="fragment"  />
    </div>
</div>



### React is V in MVC.. oh wait, not anymore

<img src="img/react-commit.png" style="max-width: 80%;" />



### Экосистема React - Redux

<img src="img/react-redux-diagram.png" />



### Чтение на лето

 - [Habr: Охота на мифический MVC - 1](https://habr.com/ru/post/321050/)
 - [Habr: Охота на мифический MVC - 2](https://habr.com/ru/post/322700/)
 - Ссылка на доклад:

<img src="img/link-to-report.svg" style="width: 25%;" />
