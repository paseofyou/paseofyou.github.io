# CompletableFuture

 CompletableFuture 是jdk8的新特性。CompletableFuture实现了CompletionStage接口和Future接口，前者是对后者的一个扩展，增加了异步会点、流式处理、多个Future组合处理的能力，使Java在处理多任务的协同工作时更加顺畅便利。

## 一、创建异步任务

### 1. supplyAsync

supplyAsync是创建带有返回值的异步任务。它有如下两个方法，一个是使用默认线程池（ForkJoinPool.commonPool()）的方法，一个是带有自定义线程池的重载方法

```java
// 带返回值异步请求，默认线程池
public static <U> CompletableFuture<U> supplyAsync(Supplier<U> supplier)
 
// 带返回值的异步请求，可以自定义线程池
public static <U> CompletableFuture<U> supplyAsync(Supplier<U> supplier, Executor executor)
```

测试代码：

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> cf = CompletableFuture.supplyAsync(() -> {
            System.out.println("do something....");
            return "result";
        });
 
        //等待任务执行完成
        System.out.println("结果->" + cf.get());
}
 
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        // 自定义线程池
        ExecutorService executorService = Executors.newSingleThreadExecutor();
        CompletableFuture<String> cf = CompletableFuture.supplyAsync(() -> {
            System.out.println("do something....");
            return "result";
        }, executorService);
 
        //等待子任务执行完成
        System.out.println("结果->" + cf.get());
}
```

### 2. runAsync

runAsync是创建没有返回值的异步任务。它有如下两个方法，一个是使用默认线程池（ForkJoinPool.commonPool()）的方法，一个是带有自定义线程池的重载方法

```java
// 不带返回值的异步请求，默认线程池
public static CompletableFuture<Void> runAsync(Runnable runnable)
 
// 不带返回值的异步请求，可以自定义线程池
public static CompletableFuture<Void> runAsync(Runnable runnable, Executor executor)
```

测试代码：
```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Void> cf = CompletableFuture.runAsync(() -> {
            System.out.println("do something....");
        });
 
        //等待任务执行完成
        System.out.println("结果->" + cf.get());
}
 
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        // 自定义线程池
        ExecutorService executorService = Executors.newSingleThreadExecutor();
        CompletableFuture<Void> cf = CompletableFuture.runAsync(() -> {
            System.out.println("do something....");
        }, executorService);
 
        //等待任务执行完成
        System.out.println("结果->" + cf.get());
}
```

### 3.获取任务结果的方法

```java
// 如果完成则返回结果，否则就抛出具体的异常
public T get() throws InterruptedException, ExecutionException 
 
// 最大时间等待返回结果，否则就抛出具体异常
public T get(long timeout, TimeUnit unit) throws InterruptedException, ExecutionException, TimeoutException
 
// 完成时返回结果值，否则抛出unchecked异常。为了更好地符合通用函数形式的使用，如果完成此 CompletableFuture所涉及的计算引发异常，则此方法将引发unchecked异常并将底层异常作为其原因
public T join()
 
// 如果完成则返回结果值（或抛出任何遇到的异常），否则返回给定的 valueIfAbsent。
public T getNow(T valueIfAbsent)
 
// 如果任务没有完成，返回的值设置为给定值
public boolean complete(T value)
 
// 如果任务没有完成，就抛出给定异常
public boolean completeExceptionally(Throwable ex) 
 
```

##  二、异步回调处理

### 1.thenApply和thenApplyAsync

thenApply 表示某个任务执行完成后执行的动作，即回调方法，会将该任务的执行结果即方法返回值作为入参传递到回调方法中，带有返回值。

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Integer> cf2 = cf1.thenApplyAsync((result) -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
            result += 2;
            return result;
        });
        //等待任务1执行完成
        System.out.println("cf1结果->" + cf1.get());
        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
}
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Integer> cf2 = cf1.thenApply((result) -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
            result += 2;
            return result;
        });
        //等待任务1执行完成
        System.out.println("cf1结果->" + cf1.get());
        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
}
```

 thenApply 和 thenApplyAsync 区别在于，使用 thenApply 方法时子任务与父任务使用的是同一个线程，而 thenApplyAsync 在子任务中是另起一个线程执行任务，并且 thenApplyAsync 可以自定义线程池，默认的使用 ForkJoinPool.commonPool() 线程池。

同步调用 (我们通常使用的那种) 意味着：“当你完成工作时，才返回”，而异步调用以意味着： “立刻返回并继续后续工作”。 正如你所看到的，`cf` 的创建现在发生的更快。每次调用 `thenApplyAsync()` 都会立刻返回，因此可以进行下一次调用，整个调用链路完成速度比以前快得多。

事实上，如果没有回调 `cf.join()` 方法，程序会在完成其工作之前退出。而 `cf.join()` 直到 cf 操作完成之前，阻止 `main()` 进程结束。

### 2.thenAccept和thenAcceptAsync

 thenAccept 表示某个任务执行完成后执行的动作，即回调方法，会将该任务的执行结果即方法返回值作为入参传递到回调方法中，无返回值。

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Void> cf2 = cf1.thenAccept((result) -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
        });
 
        //等待任务1执行完成
        System.out.println("cf1结果->" + cf1.get());
        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
}
 
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Void> cf2 = cf1.thenAcceptAsync((result) -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
        });
 
        //等待任务1执行完成
        System.out.println("cf1结果->" + cf1.get());
        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
}
```

 thenAccep 和 thenAccepAsync 区别在于，使用 thenAccep 方法时子任务与父任务使用的是同一个线程，而 thenAccepAsync 在子任务中可能是另起一个线程执行任务，并且 thenAccepAsync 可以自定义线程池，默认的使用 ForkJoinPool.commonPool() 线程池。

### 2.thenRun和thenRunAsync

  thenRun 表示某个任务执行完成后执行的动作，即回调方法，无入参，无返回值。

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Void> cf2 = cf1.thenRun(() -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
        });
 
        //等待任务1执行完成
        System.out.println("cf1结果->" + cf1.get());
        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
}
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Void> cf2 = cf1.thenRunAsync(() -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
        });
 
        //等待任务1执行完成
        System.out.println("cf1结果->" + cf1.get());
        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
}
```

 thenRun 和 thenRunAsync 区别在于，使用 thenRun 方法时子任务与父任务使用的是同一个线程，而 thenRunAsync 在子任务中可能是另起一个线程执行任务，并且 thenRunAsync 可以自定义线程池，默认的使用 ForkJoinPool.commonPool() 线程池。

### 3.whenComplete和whenCompleteAsync

 whenComplete 是当某个任务执行完成后执行的回调方法，会将执行结果或者执行期间抛出的异常传递给回调方法，如果是正常执行则异常为null，回调方法对应的 CompletableFuture 的 result 和该任务一致，如果该任务正常执行，则 get 方法返回执行结果，如果是执行异常，则 get 方法抛出异常。

```java
 public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            int a = 1/0;
            return 1;
        });
 
        CompletableFuture<Integer> cf2 = cf1.whenComplete((result, e) -> {
            System.out.println("上个任务结果：" + result);
            System.out.println("上个任务抛出异常：" + e);
            System.out.println(Thread.currentThread() + " cf2 do something....");
        });
 
//        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
    }
```

 whenCompleteAsync 和 whenComplete 区别也是 whenCompleteAsync 可能会另起一个线程执行任务，并且 thenRunAsync 可以自定义线程池，默认的使用 ForkJoinPool.commonPool() 线程池。

### 4.handle和handleAsync

跟whenComplete基本一致，区别在于handle的回调方法有返回值。

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            // int a = 1/0;
            return 1;
        });
 
        CompletableFuture<Integer> cf2 = cf1.handle((result, e) -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
            System.out.println("上个任务结果：" + result);
            System.out.println("上个任务抛出异常：" + e);
            return result+2;
        });
 
        //等待任务2执行完成
        System.out.println("cf2结果->" + cf2.get());
}
```

### 综合总结

前提（只是方便展示的工具类）

```java
package onjava;
import java.util.concurrent.*;
public class CompletableUtilities {
  // Get and show value stored in a CF:
  public static void showr(CompletableFuture<?> c) {
    try {
      System.out.println(c.get());
    } catch(InterruptedException
            | ExecutionException e) {
      throw new RuntimeException(e);
    }
  }
  // For CF operations that have no value:
  public static void voidr(CompletableFuture<Void> c) {
    try {
      c.get(); // Returns void
    } catch(InterruptedException
            | ExecutionException e) {
      throw new RuntimeException(e);
    }
  }
}
```

以下为总结：

```java
// concurrent/CompletableOperations.java
import java.util.concurrent.*;
import static onjava.CompletableUtilities.*;
public class CompletableOperations {
    static CompletableFuture<Integer> cfi(int i) {
        return
                CompletableFuture.completedFuture(
                        Integer.valueOf(i));
    }
    public static void main(String[] args) {
        // 演示了 showr() 正常工作
        showr(cfi(1));
        
        // 调用 runAsync() 的示例。由于 Runnable 不产生返回值，因此使用了返回 CompletableFuture <Void> 的voidr() 方法。
        voidr(cfi(2).runAsync(() ->
                System.out.println("runAsync")));
        
        // thenRunAsync() 效果似乎与 上例 cfi(2) 使用的 runAsync()相同。
        voidr(cfi(3).thenRunAsync(() ->
                System.out.println("thenRunAsync")));
        
        // runAsync() 是一个 static 方法，所以你通常不会像cfi(2)一样调用它。相反你可以在 QuittingCompletable.java 中使用它。
        voidr(CompletableFuture.runAsync(() ->
                System.out.println("runAsync is static")));
        
        // supplyAsync() 也是静态方法，区别在于它需要一个 Supplier 而不是Runnable, 并产生一个CompletableFuture<Integer> 而不是 CompletableFuture<Void>
        showr(CompletableFuture.supplyAsync(() -> 99));
        
        // then 系列方法将对现有的 CompletableFuture<Integer> 进一步操作。
        // 与 thenRunAsync() 不同，cfi(4)，cfi(5) 和cfi(6) “then” 方法的参数是未包装的 Integer。
        // AcceptAsync()接收了一个 Consumer，因此不会产生结果。
        voidr(cfi(4).thenAcceptAsync(i -> System.out.println("thenAcceptAsync: " + i)));
        
        // thenApplyAsync() 接收一个Function, 并生成一个结果（该结果的类型可以不同于其输入类型）
        showr(cfi(5).thenApplyAsync(i -> i + 42));
        
        // thenComposeAsync() 与 thenApplyAsync()非常相似，唯一区别在于其 Function 必须产生已经包装在CompletableFuture中的结果。
        showr(cfi(6).thenComposeAsync(i -> cfi(i + 99)));
        
        //演示了 obtrudeValue()，它强制将值作为结果。
        CompletableFuture<Integer> c = cfi(7);
        c.obtrudeValue(111);
        showr(c);
        
        //  使用 toCompletableFuture() 从 CompletionStage 生成一个CompletableFuture。
        showr(cfi(8).toCompletableFuture());
        
        c = new CompletableFuture<>();
        // c.complete(9) 显示了如何通过给它一个结果来完成一个task（future）（与 obtrudeValue() 相对，后者可能会迫使其结果替换该结果）。
        c.complete(9);
        showr(c);
        
        //  CompletableFuture中的 cancel()方法，如果已经完成此任务，则正常结束。 如果尚未完成，则使用 CancellationException 完成此 CompletableFuture。
        c = new CompletableFuture<>();
        c.cancel(true);
        System.out.println("cancelled: " + c.isCancelled());
        System.out.println("completed exceptionally: " + c.isCompletedExceptionally());
        System.out.println("done: " + c.isDone());
        System.out.println(c);
        
        // 任务（future）完成，则 getNow() 方法返回CompletableFuture的完成值，否则返回getNow()的替换参数。
        c = new CompletableFuture<>();
        System.out.println(c.getNow(777));
        
        // 依赖 (dependents) 的概念。
        // 如果我们将两个thenApplyAsync()调用链路到CompletableFuture上，则依赖项的数量不会增加，保持为 1。
        // 但是，如果我们另外将另一个thenApplyAsync()直接附加到c，则现在有两个依赖项：两个一起的链路和另一个单独附加的链路。
        // 这表明你可以使用一个CompletionStage，当它完成时，可以根据其结果派生多个新任务。
        c = new CompletableFuture<>();
        c.thenApplyAsync(i -> i + 42)
                .thenApplyAsync(i -> i * 12);
        System.out.println("dependents: " +
                c.getNumberOfDependents());
        c.thenApplyAsync(i -> i / 2);
        System.out.println("dependents: " +
                c.getNumberOfDependents());
    }
}
```



## 三、多任务组合处理 

### 1.thenCombine、thenAcceptBoth 和runAfterBoth

这三个方法都是将两个 CompletableFuture 组合起来处理，只有两个任务都正常完成时，才进行下阶段任务。

区别： 

- thenCombine 会将两个任务的执行结果作为方法入参，且该方法**有返回值**； 
- thenAcceptBoth 同样将两个任务的执行结果作为方法入参，但是**无返回值**； 
- runAfterBoth **没有入参**，也**没有返回值**。
- 注意: 两个任务中只要有一个执行异常，则将该异常信息作为指定任务的执行结果。

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Integer> cf2 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
            return 2;
        });
 
        CompletableFuture<Integer> cf3 = cf1.thenCombine(cf2, (a, b) -> {
            System.out.println(Thread.currentThread() + " cf3 do something....");
            return a + b;
        });
 
        System.out.println("cf3结果->" + cf3.get());
}
 
 public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Integer> cf2 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
            return 2;
        });
        
        CompletableFuture<Void> cf3 = cf1.thenAcceptBoth(cf2, (a, b) -> {
            System.out.println(Thread.currentThread() + " cf3 do something....");
            System.out.println(a + b);
        });
 
        System.out.println("cf3结果->" + cf3.get());
}
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<Integer> cf1 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf1 do something....");
            return 1;
        });
 
        CompletableFuture<Integer> cf2 = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread() + " cf2 do something....");
            return 2;
        });
 
        CompletableFuture<Void> cf3 = cf1.runAfterBoth(cf2, () -> {
            System.out.println(Thread.currentThread() + " cf3 do something....");
        });
 
        System.out.println("cf3结果->" + cf3.get());
}
```

### 2.applyToEither、acceptEither和runAfterEither

也是将两个 CompletableFuture 组合起来处理，当有一个任务正常完成时，就会进行下阶段任务。

区别： applyToEither 会将已经完成任务的执行结果作为所提供函数的参数，且该方法有返回值； acceptEither 同样将已经完成任务的执行结果作为方法入参，但是无返回值； runAfterEither 没有入参，也没有返回值。

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> cf1 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf1 do something....");
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            return "cf1 任务完成";
        });
 
        CompletableFuture<String> cf2 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf2 do something....");
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            return "cf2 任务完成";
        });
 
        CompletableFuture<String> cf3 = cf1.applyToEither(cf2, (result) -> {
            System.out.println("接收到" + result);
            System.out.println(Thread.currentThread() + " cf3 do something....");
            return "cf3 任务完成";
        });
 
        System.out.println("cf3结果->" + cf3.get());
}
 
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> cf1 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf1 do something....");
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            return "cf1 任务完成";
        });
 
        CompletableFuture<String> cf2 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf2 do something....");
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            return "cf2 任务完成";
        });
 
        CompletableFuture<Void> cf3 = cf1.acceptEither(cf2, (result) -> {
            System.out.println("接收到" + result);
            System.out.println(Thread.currentThread() + " cf3 do something....");
        });
 
        System.out.println("cf3结果->" + cf3.get());
}
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> cf1 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf1 do something....");
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf1 任务完成");
            return "cf1 任务完成";
        });
 
        CompletableFuture<String> cf2 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf2 do something....");
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf2 任务完成");
            return "cf2 任务完成";
        });
 
        CompletableFuture<Void> cf3 = cf1.runAfterEither(cf2, () -> {
            System.out.println(Thread.currentThread() + " cf3 do something....");
            System.out.println("cf3 任务完成");
        });
 
        System.out.println("cf3结果->" + cf3.get());
}
```

使用 applyToEither 组合两个任务时，只要有其中一个任务完成时，就会执行 cf3 任务，显然 cf1 任务先完成了并且将自己任务的结果传值给了 cf3 任务， cf3 任务中打印了接收到 cf1 任务完成，接着完成自己的任务，并返回 cf3 任务完成； acceptEither 和 runAfterEither 类似， acceptEither 会将cf1任务的结果作为cf3任务的入参，但cf3任务完成时并无返回值； runAfterEither 不会将 cf1 任务的结果作为 cf3 任务的入参，它是没有任务入参，执行完自己的任务后也并无返回值。

### 3.allOf / anyOf

allOf：CompletableFuture是多个任务都执行完成后才会执行，只有有一个任务执行异常，则返回的CompletableFuture执行get方法时会抛出异常，如果都是正常执行，则get返回null。

anyOf ：CompletableFuture是多个任务只要有一个任务执行完成，则返回的CompletableFuture执行get方法时会抛出异常，如果都是正常执行，则get返回执行完成任务的结果。

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> cf1 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf1 do something....");
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf1 任务完成");
            return "cf1 任务完成";
        });
 
        CompletableFuture<String> cf2 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf2 do something....");
                int a = 1/0;
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf2 任务完成");
            return "cf2 任务完成";
        });
 
        CompletableFuture<String> cf3 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf2 do something....");
                Thread.sleep(3000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf3 任务完成");
            return "cf3 任务完成";
        });
 
        CompletableFuture<Void> cfAll = CompletableFuture.allOf(cf1, cf2, cf3);
        System.out.println("cfAll结果->" + cfAll.get());
}
 
 
public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> cf1 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf1 do something....");
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf1 任务完成");
            return "cf1 任务完成";
        });
 
        CompletableFuture<String> cf2 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf2 do something....");
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf2 任务完成");
            return "cf2 任务完成";
        });
 
        CompletableFuture<String> cf3 = CompletableFuture.supplyAsync(() -> {
            try {
                System.out.println(Thread.currentThread() + " cf2 do something....");
                Thread.sleep(3000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("cf3 任务完成");
            return "cf3 任务完成";
        });
 
        CompletableFuture<Object> cfAll = CompletableFuture.anyOf(cf1, cf2, cf3);
        System.out.println("cfAll结果->" + cfAll.get());
}
```

