# Observables
Types of Observables

```kotlin
private fun dummyBook() : ArrayList<Book>{
    var books = arrayListOf<Book>()
    books.add(Book("Why is the snail slow?", "Alex"))
    books.add(Book("Clean code", "David"))
    return books
}
```

# Observable & Observer
- Emit empty or multiple item
- Example:
```kotlin
Observable.create<Book> {
    it.onNext(Book("Why is the snail slow?", "Alex"))
}.subscribe(object : Observer<Book> {
    override fun onComplete() {
        println("onComplete")
    }

    override fun onSubscribe(d: Disposable) {
        println("onSubscribe")
    }

    override fun onNext(t: Book) {
        println("onNext: $t")
    }

    override fun onError(e: Throwable) {
        println("error: ${e.message}")
    } 
})
```
- Result:
```
onNext: Book(name=Why is the snail slow?, author=Alex)
```
# Single & SingleObsever
![Image of Single](https://raw.githubusercontent.com/wiki/ReactiveX/RxJava/images/rx-operators/Single.create.png)
- Always emit one item or onError
- Example:
```kotlin
Single.create<Book> {
    it.onSuccess(Book("Why is the snail slow?", "Alex"))
}.subscribe(object : SingleObserver<Book> {
    override fun onSuccess(t: Book) {
        println("success: $t")
    }

    override fun onSubscribe(d: Disposable) {

    }

    override fun onError(e: Throwable) {
        println("error: ${e.message}")
    }
})
```
- Result:
```
success: Book(name=Why is the snail slow?, author=Alex)
```
# Maybe & MaybeObserver
![Image of Maybe](https://raw.githubusercontent.com/wiki/ReactiveX/RxJava/images/rx-operators/maybe.png)
- Emit one or none item
- Example:
```kotlin
Maybe.create<Book> {
    it.onSuccess(Book("Why is the snail slow?", "Alex"))
}.subscribe(object : MaybeObserver<Book> {
    override fun onSuccess(t: Book) {
        println("success: $t")
    }

    override fun onComplete() {
        println("onComplete")
    }

    override fun onSubscribe(d: Disposable) {
        println("onSubscribe")
    }

    override fun onError(e: Throwable) {
        println("error: ${e.message}")
    }

})
```
- Result:
```
success: Book(name=Why is the snail slow?, author=Alex)
```
# Completable & CompletableObserver
![Image of Completable](https://cdn-images-1.medium.com/max/2400/1*46zvx16PObtTWlUxKwVkyA.png)
- Emit none item
- Example:
```kotlin
Completable.create {
    it.onComplete()
}.subscribe(object : CompletableObserver{
    override fun onComplete() {
        println("onComplete")
    }

    override fun onSubscribe(d: Disposable) {
        println("onSubscribe")
    }

    override fun onError(e: Throwable) {
        println("onError: ${e.message}")
    }

})
```
- Result:
```
System.out: onComplete
```
