title: ReactiveX 学习二：RxJs中Observable的使用（Angular2）
date: 2017-8-5
tags:
- ReactiveX
- RxJs
- Observable
----

## Observable 

> RxJS with Angular2

> We can use RxJS observables inside Angular2 services. It allows your components to subscribe and be informed when data changes.

> Angular2 is really linked to RxJS (which is in version 5 beta 1) and promotes it. You can use RxJS observables to build stores-like inside a Angular2 application.

1.Angular2 Observable data services.
2.Managing state in Angular 2 using RxJs.
3.Reactive Data Flow in Angular 2
4.Managing state in Angular2 using RxJS in a Redux-like way

## Observable订阅后需要取消订阅?

比如我们需要一个待办事项的数据服务，如下定义；
```
// Todo Service
export class TodoService {

	get fetchTodo(date: string): Observable<any> {
		const api = "http://xxx/todos/" + date;
		return http.get(api);
	}
}

```

在Angular组件中，一个方法`load()`使用的该服务，产生了订阅。
```
import {TodoService} from './todo-service';

@Component({
    selector: 'todo', // 自定义的标签名
    styleUrls: [],
    providers: []
})
export class TodoComponent implements  {
	
	private _todos: Todo[];

	// Angular 依赖自动注入
	constructor(private todoService: TodoService) {        
    }

    load(date: string) {
		todoService.fetchTodo.map(item => item.json()).subscribe( ret => {
			this._todos = ret.todos;
		});
    }
}

```
在以上的例子中，因为是HTTP请求。


## 需要考虑的问题

- 是否Observable发送了complete事件，subscribe操作就完成了，也自动完成了unsubscribe，也释放了资源?
- 


## 单向数据流

<img src="https://docs.google.com/drawings/d/1UMNTBHz_XXJtDAon1QmC5Y5JfXTtS1j8wDW6u2fAvlg/pub?w=1002&amp;h=600">

## 参考资料

[Angular2: Select a state management strategy](https://bertrandg.github.io/angular2-application-state-management-strategy/)  
[Reactive Data Flow in Angular 2](https://lambda-it.ch/blog/post/reactive-data-flow-in-angular-2)  
[Angular/RxJs When should I unsubscribe from `Subscription`](https://stackoverflow.com/questions/38008334/angular-rxjs-when-should-i-unsubscribe-from-subscription) 