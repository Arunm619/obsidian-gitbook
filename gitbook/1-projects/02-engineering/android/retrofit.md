
Making Retrofit work for you 

Jake Wharton - 2016

Slides - [Making Retrofit Work For You (Ohio DevFest 2016) - Speaker Deck](https://speakerdeck.com/jakewharton/making-retrofit-work-for-you-ohio-devfest-2016)
JW - [Making Retrofit Work For You by Jake Wharton - YouTube](https://www.youtube.com/watch?v=t34AQlblSeE&t=3080s&ab_channel=GDGCincinnati)

Retrofit is a java library by Square. 
- Not android specific. 
- Android apps and server apps (written in java)

Agenda 
- Leverage the library to make it do more work for you
- discuss not so common library features


An abstraction on some remote API.
Services needs to communicate with other services or remote APIs. 

```kotlin
interface GithubAPI {
fun getUsers(request: Request): List<User>
}
```

Implementing the `GithubAPI` interface using `HttpURLConnection` in Kotlin. Here's a simple implementation:

```kotlin
import java.io.BufferedReader
import java.io.InputStreamReader
import java.net.HttpURLConnection
import java.net.URL

class GithubAPIImpl : GithubAPI {
    override fun getUsers(request: Request): List<User> {
        val url = URL(request.url)
        val connection = url.openConnection() as HttpURLConnection

        connection.requestMethod = "GET"
        connection.setRequestProperty("Content-Type", "application/json; utf-8")
        connection.setRequestProperty("Accept", "application/json")

        val responseCode = connection.responseCode
        if (responseCode == HttpURLConnection.HTTP_OK) {
            BufferedReader(InputStreamReader(connection.inputStream)).use {
                val response = it.readText()
                // Parse the response to a list of User objects
                // This depends on the structure of your User class and the response
                // Here, I'm returning an empty list as a placeholder
                return listOf<User>()
            }
        } else {
            throw RuntimeException("Failed : HTTP error code : $responseCode")
        }
    }
}
```

This is a basic example and doesn't include error handling or connection timeouts. You'll also need to replace the placeholder code that parses the response into a list of `User` objects with actual parsing code.

Now, if you want to implement the same using Retrofit, you would do something like this:

```kotlin
import retrofit2.Call
import retrofit2.http.GET

interface GithubAPI {
    @GET("users")
    fun getUsers(): Call<List<User>>
}
```

In Retrofit, you define your API as an interface with methods for each endpoint. Each method is annotated with an HTTP annotation (like `@GET`, `@POST`, etc.) that specifies the request type and the relative URL. The return type is `Call<T>`, where `T` is the type of the response body.

You would then use a `Retrofit.Builder` to create an instance of this interface and call its methods to send requests.

---

Instead of writing HttpUrl implementation ourselves, we want retrofit to programatically generate that for us.

we want to add a metadata to it with annotations and then code-gen will do its job.

>In retrofit 2, the response is forced to be wrapped in `Call` object so that we can decide if we want it to be processed synchronously or asynchronously.

>`Call` is a type used in Retrofit, a type-safe HTTP client for Android and Java. It represents a single request and the response it will generate. `Call<T>` is a parameterized type where `T` is the type of the response body. 

>When you define a method in a Retrofit interface to send a network request, you typically declare it to return a `Call<T>`. This allows you to send the request and receive the response asynchronously with `enqueue()`, or synchronously with `execute()`. 

>In the context of your `GithubAPI` interface, `Call<List<User>>` means that the `getUsers()` method will return a `Call` object that, when executed, will make a network request and return a `List<User>` as the response body.


----
**Annotations**

| Annotation | Explanation | Usage Code |
| --- | --- | --- |
| `@GET` | Used to send a GET request to the server. | `@GET("users") fun getUsers(): Call<List<User>>` |
| `@POST` | Used to send a POST request to the server. | `@POST("users/new") fun createUser(@Body user: User): Call<User>` |
| `@PUT` | Used to send a PUT request to the server. | `@PUT("users/{id}") fun updateUser(@Path("id") id: Int, @Body user: User): Call<User>` |
| `@DELETE` | Used to send a DELETE request to the server. | `@DELETE("users/{id}") fun deleteUser(@Path("id") id: Int): Call<Void>` |
| `@PATCH` | Used to send a PATCH request to the server. | `@PATCH("users/{id}") fun updateUserPartial(@Path("id") id: Int, @Body user: User): Call<User>` |
| `@HEAD` | Used to send a HEAD request to the server. | `@HEAD("users/{id}") fun getUserHead(@Path("id") id: Int): Call<Void>` |
| `@OPTIONS` | Used to send an OPTIONS request to the server. | `@OPTIONS("users/{id}") fun getUserOptions(@Path("id") id: Int): Call<Void>` |
| `@HTTP` | Used to send a request with a custom method to the server. | `@HTTP(method = "CUSTOM", path = "users/{id}", hasBody = true) fun customMethod(@Path("id") id: Int, @Body user: User): Call<User>` |
| `@Body` | Used to specify the body of a POST/PUT/PATCH request. | `fun createUser(@Body user: User): Call<User>` |
| `@Path` | Used to replace a placeholder in the URL path. | `@GET("users/{id}") fun getUser(@Path("id") id: Int): Call<User>` |
| `@Query` | Used to add a query parameter to the URL. | `@GET("users") fun getUsers(@Query("sort") sort: String): Call<List<User>>` |
| `@QueryMap` | Used to add multiple query parameters to the URL. | `@GET("users") fun getUsers(@QueryMap options: Map<String, String>): Call<List<User>>` |
| `@Field` | Used to send form-urlencoded data in a POST request. | `@FormUrlEncoded @POST("user/edit") fun updateUser(@Field("first_name") first: String, @Field("last_name") last: String): Call<User>` |
| `@FieldMap` | Used to send multiple form-urlencoded data in a POST request. | `@FormUrlEncoded @POST("user/edit") fun updateUser(@FieldMap fields: Map<String, String>): Call<User>` |
| `@Part` | Used to send multipart data in a POST request. | `@Multipart @POST("upload") fun upload(@Part file: MultipartBody.Part): Call<ResponseBody>` |
| `@PartMap` | Used to send multiple multipart data in a POST request. | `@Multipart @POST("upload") fun upload(@PartMap parts: Map<String, @JvmSuppressWildcards RequestBody>): Call<ResponseBody>` |
| `@Header` | Used to add a header to the request. | `@GET("user") fun getUser(@Header("Authorization") auth: String): Call<User>` |
| `@Headers` | Used to add multiple headers to the request. | `@Headers("Accept: application/json", "User-Agent: Retrofit-Sample-App") @GET("user") fun getUser(): Call<User>` |
| `@Url` | Used to pass a full URL for a request. | `@GET fun getUser(@Url url: String): Call<User>` |

Please note that this is not an exhaustive list and there are other annotations available in Retrofit.

----

How to take the interface into something that makes the request. 

Introducing Retrofit Object.

```kotlin
import okhttp3.OkHttpClient
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

val okHttpClient = OkHttpClient.Builder()
    .build()

val retrofit = Retrofit.Builder()
    .baseUrl("https://api.github.com/") // replace with your base URL
    .client(okHttpClient)
    .addConverterFactory(GsonConverterFactory.create())
    .build()

val githubAPI = retrofit.create(GithubAPI::class.java)
```

interfaces are referred to as services.

Call object is parameterised on list of users. 
Retrofit handles the conversion automatically. 


Configurations of Retrofit object
Retrofit is not a http client itself, it delegates to the http client.
Retrofit parses the interfaces, learns how to make the request, makes them and asks the client to make them for it. 

Http client - OkHttpClient.

Logically we may want to separate the services. 

```kotlin
val foo = retrofit.create(Foo::class.java)
val bar = retrofit.create(Bar::class.java)
```

Examples
- Checkout Service
- Address Service
- Order Service
- Feed Service 

---
What if we need two different base urls?


```kotlin
val retrofit = Retrofit.Builder()
    .baseUrl("https://api.foo.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build()
val foo = retrofit.create(Foo::class.java)  
```

Like this:
```kotlin
val retrofitFoo = Retrofit.Builder()
    .baseUrl("https://api.foo.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build()
val foo = retrofit.create(Foo::class.java)

val retrofitBar = Retrofit.Builder()
    .baseUrl("https://api.bar.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build()
val bar = retrofit.create(Bar::class.java)
```

But in this case, we are implicitly creating two different underlying okHttpClient which is bad because it does some pretty smart things that gets broken now.

Smart things that OkHttpClient does:

1. Disk caching
2. connection pooling
3. route database (path of best way to connect to the server)
4. Split brain problem (no longer sharing).

```kotlin
val client = OkHttpClient()
val retrofitFoo = Retrofit.Builder()
    .baseUrl("https://api.foo.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .client(client)
    .build()
val foo = retrofit.create(Foo::class.java)

val retrofitBar = Retrofit.Builder()
    .baseUrl("https://api.bar.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .client(client)
    .build()
val bar = retrofit.create(Bar::class.java)
```
Classic solve: Use singleton for the client to retain the benefits.

---

Http client 

Default client is OkHttp for Retrofit. 

```kotlin
val client = OkHttpClient()
val clientFoo = client.newBuilder()
				.addInterceptor(FooInterceptor())
				.build()
val clientBar = client.newBuilder()
				.readTimeOut(30, SECONDS)
				.writeTimeOut(30, SECONDS)
				.build()

```

client and clientFoo share the same underlying client with extra configs.
bar - server is in another side of the world. 

These are shallow copies. `client` is baseline configurations.

same client means sharing
1. Disk caching
2. connection pooling
3. route database (path of best way to connect to the server)


----
How to determine which APIs needs auth or not.
one way is to keep a check in the interceptor if its a particular X=login API then we need to authenticate otherwise for every API we need to authenticate. 


```kotlin

inteface Service {
@GET("/user") // auth required
fun getUser() : Call<User>

@POST("/login") // no auth required
fun login(@Body request: LoginRequest) : Call<User>
}
```

This problem creates tight couping between service interface and interceptor. We need to remember and update things. 

Better solution would be to :

**Marker Header.** 

```kotlin

inteface Service {
@GET("/user")
fun getUser() : Call<User>

@POST("/login")
@Headers("No-Authentication: true")
fun login(@Body request: LoginRequest) : Call<User>

}
```

and then in the interceptor :

```kotlin
class ServiceInterceptor: Interceptor {
override fun intercept(chain: Chain): Response {
	   val request = chain.request()
	   if(request.header("No-Authentication") == null) {
	   request = request.newBuilder()
			     .addHeader("Authorization", "619")
			     .build()
	   }
	   return chain.proceed(request);
}
}
```

- Logging metrics 
- Gzip request bodies (okhttp doesn't do by default).

---
**Converters***

Convert objects to and from their representation in HTTP. Instances are created by a factory which is installed into the Retrofit instance.

```java
public interface Converter<F, T> {  
  @Nullable  
  T convert(F value) throws IOException;  
  
  abstract class Factory {
  //responseBodyConverter bytes to Java
  public @Nullable Converter<ResponseBody, ?> responseBodyConverter(  
    Type type, Annotation[] annotations, Retrofit retrofit) {  
  return null;  //can't handle
}

  //requestBodyConverter java to bytes
  public @Nullable Converter<?, RequestBody> requestBodyConverter(  
    Type type,  
    Annotation[] parameterAnnotations,  
    Annotation[] methodAnnotations,  
    Retrofit retrofit) {  
  return null;  //can't handle
}

//string converter bytes to string
public @Nullable Converter<?, String> stringConverter(  
    Type type, Annotation[] annotations, Retrofit retrofit) {  
  return null;   //can't handle
}

Type getParameterUpperBound(int index, ParameterizedType type) {

}

Class<?> getRawType(Type type)

  }
```


Takes the bytes into nice java bits 
and vice versa. 

`ResponseBody` is the object that represents the bytes from the network. 

```
Call<ResponseBody>
```
```kotlin
val retrofit = Retrofit.Builder()
    .baseUrl("https://api.foo.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build()
val foo = retrofit.create(Foo::class.java)  
``` 


A converter in Retrofit is used for serialization and deserialization of objects. It's responsible for converting the data received from the server into a usable data model and vice versa. Retrofit doesn't have a built-in converter for JSON, so you need to add a converter library to handle this. 

Moshi is one of the libraries that Retrofit can use to convert JSON into Java or Kotlin objects. It's a modern JSON library for Android and Java, and it can work with Kotlin's classes seamlessly. It's developed by Square, the same company that developed Retrofit, and is often used as an alternative to Gson.

To use Moshi with Retrofit, you need to add the Moshi converter library to your project and then add it to your Retrofit instance using the `addConverterFactory()` method. Here's an example:

```kotlin
import com.squareup.moshi.Moshi
import retrofit2.Retrofit
import retrofit2.converter.moshi.MoshiConverterFactory

val moshi = Moshi.Builder().build()

val retrofit = Retrofit.Builder()
    .baseUrl("https://api.github.com/")
    .addConverterFactory(MoshiConverterFactory.create(moshi))
    .build()
```

In this code, `MoshiConverterFactory.create(moshi)` tells Retrofit to use Moshi for JSON conversion.

Moshi supports many of the same features as Gson, such as custom serializers/deserializers and annotations, but it's generally more up-to-date with modern language features and has better performance. It also has better support for Kotlin, including built-in support for Kotlin's non-nullable types and default values.


Make sure the MoshiConvertor is Singleton as the internal machinery is put to best use when shared and to avoid the split brain problem.

We can add multiple converter factories. 
- ProtoConverter 
- GsonConverter
- MoshiConverter
- SimpleXMLConverter


This works in sequence. Whenever a type is being able to be handled by a converter it will pick it up else it will pass.
Behaviour should be known and based on that the order should be set. Order matters.

XML converter and Gson Converter always say yes to convert anything to everything.

so what do we do in this case?

```
new XMLOrJsonConverterFactory()

Use annotations to identify the type and give the right Converter.
```
![[Screenshot 2024-03-21 at 12.41.44 AM.png]]

Proto is generated class and it extends from a type.

On the wire - from the network.

Usually the data from the network is wrapped is what we call as "Envelope", basically just some metadata surrounding the actual response. 

Solution EnvelopeConverter Factory. 

---
Ruby server returns 0 bytes. 
Protocol buffers 0 bytes is a valid response. 
Json object 0 bytes is invalid. `{}` only this is valid. 
`NULL` is also valid.

---
Plaid converters

Converter was created to fix the missing search api. Hits the website and converts jsoup to object to list of type.

---
### Call Adapters


```java
/**  
 * Adapts a {@link Call} with response type {@code R} into the type of {@code T}. Instances are  
 * created by {@linkplain Factory a factory} which is {@linkplain  
 * Retrofit.Builder#addCallAdapterFactory(Factory) installed} into the {@link Retrofit} instance.  
 */public interface CallAdapter<R, T> {  
  /**  
   * Returns the value type that this adapter uses when converting the HTTP response body to a Java   * object. 
   */
    Type responseType();  
  
  /**  
   * Returns an instance of {@code T} which delegates to {@code call}.  */  
  T adapt(Call<R> call);  
  
  /**  
   * Creates {@link CallAdapter} instances based on the return type of {@linkplain  
   * Retrofit#create(Class) the service interface} methods.  
   */  abstract class Factory {  
    /**  
     * Returns a call adapter for interface methods that return {@code returnType}, or null if it  
     * cannot be handled by this factory.     */    public abstract @Nullable CallAdapter<?, ?> get(  
        Type returnType, Annotation[] annotations, Retrofit retrofit);  
  
    /**  
     * Extract the upper bound of the generic parameter at {@code index} from {@code type}. For  
     * example, index 1 of {@code Map<String, ? extends Runnable>} returns {@code Runnable}.  
     */    protected static Type getParameterUpperBound(int index, ParameterizedType type) {  
      return Utils.getParameterUpperBound(index, type);  
    }  
  
    /**  
     * Extract the raw class type from {@code type}. For example, the type representing {@code  
     * List<? extends Runnable>} returns {@code List.class}.  
     */    protected static Class<?> getRawType(Type type) {  
      return Utils.getRawType(type);  
    }  
  }  
}
```

Other half of the request execution mechanism. 

Call adapters deals with the actual execution, the synchronous, the asynchronous, threading details.

Call object is the built in execution mechanism. 

```kotlin

Call<User> <--- Call <---- Call.Factory(aka OKHttpClient)
```

`Call<User>` is retrofit's call. Deals with java objects. Serialisation.
Call is OkHttp's call. Deals with raw bytes from network.

```kotlin

*Call<User> <---(Call Adapter)* Call<User> <--- Call <---- Call.Factory(aka OKHttpClient)
```

This is unintuitive. 
The original work is done in the same thread as http client. 
then while returning back to main thread, retrofit wraps it again with call object. Call adapter does this work. 

`*part*` is customisable with CallAdapter.

There are separate artefacts we can depend on. 

- RxJavaCallAdapterFactory
- CoroutineCallAdapterFactory


A Call Adapter in Retrofit is a mechanism that defines how the return types of the API interface methods are converted into actual objects. By default, Retrofit can only return `Call<T>` types from the API interface methods. However, with the help of Call Adapters, Retrofit can return other types like `Observable<T>`, `Single<T>`, `Completable`, `Deferred<T>`, etc.

Retrofit has built-in support for some call adapters like RxJava, Guava, and Java 8's CompletableFuture. You can add these call adapters to your Retrofit instance using the `addCallAdapterFactory()` method.

Here's an example of how to use the RxJava2CallAdapterFactory to allow your API interface methods to return RxJava 2 types:

```kotlin
import retrofit2.Retrofit
import retrofit2.adapter.rxjava2.RxJava2CallAdapterFactory
import retrofit2.converter.gson.GsonConverterFactory

val retrofit = Retrofit.Builder()
    .baseUrl("https://api.github.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .addCallAdapterFactory(RxJava2CallAdapterFactory.create())
    .build()
```

With this setup, you can now have API interface methods like this:

```kotlin
import io.reactivex.Single
import retrofit2.http.GET

interface GithubAPI {
    @GET("users/octocat")
    fun getUser(): Single<User>
}
```

In this example, `getUser()` returns a `Single<User>`, which is an RxJava 2 type. When you call this method, Retrofit will use the RxJava2CallAdapterFactory to convert the HTTP response into a `Single<User


fun fact: Rxajava call adapter factory is by default synchronous. 
```kotlin
RxJava2CallAdapterFactory.createWithScheduler(Schedulers.io())
```
only this will make it async.

Schedulers are basically thread pools.

`getRawType` gives generic raw type.

Single, Observable - RxJava
CompletableFuture - Java
ListenableFuture - Guava
Call - Retrofit
Create your own call adapter

----
### **Summary**

- Http client sends the bits across the wire
- Converters manipulate the request/response data
- Call adapters change execution mechanism
- Mock mode creates deterministic, fake data for testing.

---
Next? 
Rahul Pandey - [What You Didn’t Know About Retrofit with Kotlin - Android - YouTube](https://www.youtube.com/watch?v=eomdGn7XGNo&ab_channel=RahulPandey)

