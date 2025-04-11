RxJava allows for asynchronous programming by using `Observables` which represent streams of data or events. These streams can be manipulated using operators, and subscribers react to the data emitted by the Observable. This example demonstrates fetching data from an API asynchronously using RxJava, handling errors, and displaying the results in the UI. 

Java

```
import io.reactivex.Observable;
import io.reactivex.android.schedulers.AndroidSchedulers;
import io.reactivex.schedulers.Schedulers;

// Assume you have a method to fetch data from an API that returns an Observable
// Observable<String> fetchData();

public class AsyncExample {

    public void fetchDataAndDisplay() {
        // Create an Observable from a callable that fetches data
        Observable.fromCallable(this::fetchData)
                // Subscribe on the IO thread for network operations
                .subscribeOn(Schedulers.io())
                // Observe on the main thread for UI updates
                .observeOn(AndroidSchedulers.mainThread())
                // Handle errors during data fetching
                .onErrorResumeNext(throwable -> {
                    // Handle the error, e.g., display an error message
                    System.out.println("Error: " + throwable.getMessage());
                    // Return an empty Observable to continue the stream
                    return Observable.empty();
                })
                // Subscribe to the Observable and handle the emitted data
                .subscribe(data -> {
                    // Display the fetched data in the UI
                    System.out.println("Data received: " + data);
                });
    }

    // Placeholder for your API call (replace with your actual implementation)
    private Observable<String> fetchData() {
        // Simulate a network call (replace with your actual API call)
        return Observable.just("Data from API");
    }
}
```

Explanation:

1. `Observable.fromCallable(this::fetchData)`:

    Creates an `Observable` that wraps the result of the `fetchData` method, which is assumed to be a network call or an operation that takes time. 

2. `subscribeOn(Schedulers.io())`:
    
    Specifies that the `fetchData` operation (the API call) should be executed on an `IO` thread, which is suitable for network operations. 

3. `observeOn(AndroidSchedulers.mainThread())`:

    Ensures that the emitted data from the `Observable` (the result of `fetchData`) is delivered to the subscriber (the lambda) on the main (UI) thread, allowing for UI updates. 

4. `onErrorResumeNext(throwable -> Observable.empty())`:

    Handles potential errors during the API call. If an error occurs, it prints the error message and returns an empty `Observable` to prevent the stream from terminating prematurely. 

5. `.subscribe(data -> { ... })`:

    Subscribes to the `Observable` and provides a lambda expression that handles the data emitted by the `Observable`. In this case, it prints the received data to the console.

Key Concepts:

-   `Observable`: Represents a stream of data or events that can be emitted over time. 
-   `subscribeOn(scheduler)`: Specifies which thread the `Observable` will emit data from. 
-   `observeOn(scheduler)`: Specifies which thread the subscriber will receive data on. 
-   `onErrorResumeNext`: Handles errors in the stream and allows for continuation. 
-   `Schedulers`: Provides different thread pools for different types of operations (e.g., `Schedulers.io()` for IO, `Schedulers.computation()` for CPU-bound operations). 

This example demonstrates how RxJava simplifies asynchronous programming by allowing you to manage asynchronous operations, handle errors, and ensure that UI updates happen on the main thread.