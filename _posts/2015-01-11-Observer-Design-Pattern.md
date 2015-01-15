#Observer Design Pattern
The observer design pattern enables a subscriber to register with and receive notifications from a provider. 
It is suitable for any scenario that requires push-based notification.  
观察者设计模式确保订阅者可以从提供者处注册通知，并且接收通知。它适用于任何基于推送通知的情况  
 The pattern defines a provider (also known as a subject or an observable) and zero, one, or more observers.  
此模式定义了一个提供者(也被称为主题或者被观察的对象)以及0个，1个或多个观察者。  
 Observers register with the provider, and whenever a predefined condition, event, or state change occurs, the provider automatically notifies all observers by calling one of their methods.   
观察者在提供者上注册，并且当一个预定义的条件，事件或者状态改变发生时，提供者会通过调用观察者们的方法来自动通知所有的观察者  
 In this method call, the provider can also provide current state information to observers.   
通过此方法的调用，提供者也快成向观察者们提供当前的状态信息  
 In the .NET Framework, the observer design pattern is applied by implementing the generic System.IObservable<T> and System.IObserver<T> interfaces.  
 The generic type parameter represents the type that provides notification information.
在.net框架下，可以通过实现IObservable<T>和IObserver<T>泛型接口来应用观察者设计模式。泛型参数代表了提供通知信息的类型。
##Applying the Pattern
The observer design pattern is suitable for distributed push-based notifications, because it supports a clean separation between two different components or application layers, such as a data source (business logic) layer and a user interface (display) layer. 
观察者设计模式适用于分布式的基于推送的通知，因为它支持两个组件或应用层之间的完全分离，比如数据层(业务逻辑层)和用户界面层（显示层）  
The pattern can be implemented whenever a provider uses callbacks to supply its clients with current information.  
每当提供者需要使用回调来向客户端提供当前信息的时候，都可以通过此模式来实现。
Implementing the pattern requires that you provide the following:  
实现此模式要求你提供一下几点：  
1.A provider or subject, which is the object that sends notifications to observers. A provider is a class or structure that implements the IObservable<T> interface. The provider must implement a single method, IObservable<T>.Subscribe, which is called by observers that wish to receive notifications from the provider.  
提供者或主题，是向观察者们发送通知的对象。提供者是一个实现了IObservable<T>泛型接口的类或者结构。提供者必须实现一个单独的方法IObservable<T>接口中的Subscribe方法。此方法被希望从提供者处接收通知的观察者们调用。  
2.An observer, which is an object that receives notifications from a provider. An observer is a class or structure that implements the IObserver<T> interface. The observer must implement three methods, all of which are called by the provider:  
观察者是从提供者处接收通知的对象。观察者是实现了IObserver<T>泛型接口的类或结构。观察者必须实现三个方法，它们全部都由提供者来调用：  
**a**.IObserver<T>.OnNext , which supplies the observer with new or current information.  
IObserver<T>接口的OnNext方法，向观察者们提供新信息或当前信息  
**b**.IObserver<T>.OnError , which informs the observer that an error has occurred.  
IObserver<T>接口的OnError方法，用来通知观察者们，发生了一个错误  
**c**.IObserver<T>.OnCompleted , which indicates that the provider has finished sending notifications.  
IObserver<T>接口的OnCompleted方法，用来提示观察者，提供者已经发送完通知了  
3.A mechanism that allows the provider to keep track of observers.   
一个允许提供者和观察者保持联系的机制。  
Typically, the provider uses a container object, such as a System.Collections.Generic.List<T> object, to hold references to the IObserver<T> implementations that have subscribed to notifications.  
通常地，提供者使用一个容器对象（比如List<T>类型的对象）来保存订阅了通知并且实现了IObserver<T> 接口的引用。  
 Using a storage container for this purpose enables the provider to handle zero to an unlimited number of observers.  
使用存储容器的目的是为了确保提供者可以处理0到无数个观察者们。   
The order in which observers receive notifications is not defined; the provider is free to use any method to determine the order.  
观察者们接收通知的顺序不进行定义，允许提供者使用任何方式来定义观察者们接收通知的先后顺序。  
4.An IDisposable implementation that enables the provider to remove observers when notification is complete.  
实现 IDisposable接口来确保，当通知完成的时候，提供者可以移除观察者们。  
Observers receive a reference to the IDisposable implementation from the Subscribe method, so they can also call the IDisposable.Dispose method to unsubscribe before the provider has finished sending notifications.
观察者们通过Subscribe方法来获取IDisposable方法的引用，所以观察者们也可以在提供者发送完通知前，直接调用IDisposable接口的Dispose方法来取消订阅。  
5.An object that contains the data that the provider sends to its observers.   
包含提供者向观察们发送的数据的对象
The type of this object corresponds to the generic type parameter of the IObservable<T> and IObserver<T> interfaces.   
此对象的类型相当于IObservable<T>和IObserver<T>的泛型参数
Although this object can be the same as the IObservable<T> implementation, most commonly it is a separate type.  
尽管此对象可以和IObservable<T>实现相同，但是多数情况下是完全独立的类型。



##Implementing the Pattern
##Related Topics