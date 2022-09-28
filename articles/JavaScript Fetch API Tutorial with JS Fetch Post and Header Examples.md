# درس لتعلم إستخدام ال(Fetch AP) مع بعض الامثلة لإستخدام ال(JS Fetch POST) وال(Header) 

اذا كنت مبرمج يقوم ببناء تطبيقات الويب فإن احتمالية استخدامك لبعض البيانات الخارجية الداعمة لتطبيقك والمقدمة و المتاحة بالفعل بإستخدام تكنولوجيا الـ(API) من بعض الجهات الخارجية عالية جدا...

حينما ظهرت تكنولوجيا ال([AJAX](https://en.wikipedia.org/wiki/Ajax_%28programming%29)) عام 1999 احدثت ثورة في طريقة بناء تطيقات الويب وكانت نقطة انطلاق لكثير من الادوات التي نستخدمها الآن مثل (React).

في عالم تطوير المواقع ما قبل (AJAX)،كان المطور يضطر الي اعادة تحميل صفحة الويب كاملة كلما اراد عمل بعض التحديثات فالصفحة...مهما كانت تلك التحديثات بسيطة...(AJAX) اتاحت لنا طريقة سهلة يمكن من خلالها استدعاء (fetch) البيانات من الـ(back-end) واستخدام تلك البيانات في احداث التعديلات المطلوبة فالصفحة، دون الحاجة الي إعادة تحميلها...وهذا بدوره اتاح الفرصة للمبرمجين ومطوري المواقع لبناء تطبيقات اكبر واكثر تعقيدا من ذي قبل. 


## كورس سريع فال(REST APIs)

![1-9](https://www.freecodecamp.org/news/content/images/2020/08/1-9.png)

نحن نعيش الآن في عصر الـ([REST APIs](https://restfulapi.net/))...ولكن ما هو الـ(REST API)؟ بشكل مبسط...هو وسيلة يمكنك من خلالها ايداع وحفظ (push) او استدعاء (pull) البيانات من و إلي مخزن بيانات (datastore)...والمقصود هنا بالـ(datastore) هو اي شكل من اشكال تخزين البيانات سواء كان في صورة (database) او سيرفر مقدم من احد الجهات (مثل [Twitter API](https://developer.twitter.com/en/docs/twitter-api)).

هناك بعض الاختلافات مابين انواع الاوامر الخاصة بال(REST APIs). لنلقي نظرة علي الانواع الأكثر استخداما:

**GET** - وهو النوع المستخدم لإستدعاء البيانات من ال(API). علي سبيل المثال استدعاء بيانات حساب تويتر بناءا علي اسم المستخدم.

**POST** - وهو النوع المستخدم لإيداع وتخزين البيانات. علي سبيل المثال انشاء حساب تويتر جديد بإسم وعمر وايميل المستخدم.

**PUT** -  وهو النوع المستخدم لتعديل البيانات. علي سبيل المثال تعديل الايميل الخاص بالمستخدم.

**DELETE** - وهو النوع المستخدم لحذف البيانات. علي سبيل المثال حذف حساب مستخدم من قاعدة البيانات.

هناك ثلاثة عناصر أساسية في اي (REST API) وهي الطلب (resquest) والرد (response) والرأس (headers):

**الطلب (Request):** وفيه يتم إرسال بعض البيانات للـ(API) والتي تستخدم في استدعاء البيانات ذات الصلة...مثل ارسال (id) او كلمة بحثية (search word) للبحث بإستخدامها في قاعدة بيانات الـ(REST API) واستدعاء كل البيانات ذات الصلة بذلك ال(id) او بتلك الكلمة البحثية. 

![2-6](https://www.freecodecamp.org/news/content/images/2020/08/2-6.png)
*مثال لل(resquest)*


**الرد (Response):** وهي اي بيانات يقوم سيرفر الـ(REST API) بإرسالها لك في حال اذا كان طلبك ناجحا (اي وجد ما سيتوفي شروط الطلب - successful request) او عكس ذلك (لم يجد ما يستوفي شروط الطلب - failed request).

![3-5](https://www.freecodecamp.org/news/content/images/2020/08/3-5.png)
*مثال للـ(response)*


**الرأس (Headers):**  وفيه يتم إرسال اي بيانات اضافية (metadata) والتي تساعد سيرفر الـ(API) في فهم نوع الطلب الذي يتعامل معه...علي سبيل المثال، تعريف نوع المحتوي (content-type) المطلوب او الطريقة (method). 

![4-2](https://www.freecodecamp.org/news/content/images/2020/08/4-2.png)
*مثال للـ(headers)*

الميزة الحقيقية لأستخدام تكنولوجيا الـ(REST API) هي انه يمكن استخدامها لبناء مستوي واحد او طبقة واحدة (single API layer) لخدمة عدة تطبيقات في آن واحد.

علي سبيل المثال، اذا كان لديك قاعدة بيانات تريد مشاركتها ما بين تطبيق ويب وتطبيق هاتف وتطبيق PC...فكل ما تحتاجه هو إنشاء طبقة واحدة من الـ(REST API).

الأن لديك ما يكفي من المعلومات عن كيفية عمل تكنولوجيا الـ(REST API) للبدء في تعلم كيفية استخدامها...لنشرع في ذلك إذاً.


## طلب بإستخدام دالة الـ(XMLHttpRequest)
قبل ان تصبح صيغة الـ([JSON](https://www.w3schools.com/js/js_json_intro.asp)) الأكثر انتشارا واستخداما علي مستوي العالم، كان الشكل والصيغة الأساسية لتبادل البيانات هي صيغة تسمي بالـ(XML). دالة الـ(()XMLHttpResquest) هي دالة من دوال لغة الـ(JavaScript) والتي اتاحت استدعاء البيانات من الـ(API) وكانت البيانات المرسلة من الـ(API) في صيغة الـ(XML).

اتاحت تلك الدالة إمكانية استدعاء البيانات من الـ(back-end) دون الحاجة لإعادة تحميل الصفحة. هذه الدالة أصبحت الآن تدعم صيغ استدعاء أخري مثل الـ(JSON) ولم يصبح الأمر مقتصراً علي صيغة الـ(XML) فقط كما كان الآمر سابقاً.

لنبدأ بكتابة طلب (request) بإستخدام دالة الـ(()XMLHttpRequest) والتي ستستخدم الـ(Github API) لإستدعاء بيانات صفحتي الشخصية منه.


```javascript
// function to handle success
function success() {
    var data = JSON.parse(this.responseText); //parse the string to JSON
    console.log(data);
}

// function to handle error
function error(err) {
    console.log('Request Failed', err); //error details will be in the "err" object
}

var xhr = new XMLHttpRequest(); //invoke a new instance of the XMLHttpRequest
xhr.onload = success; // call success function if request is successful
xhr.onerror = error;  // call error function if request failed
xhr.open('GET', 'https://api.github.com/users/manishmshiva'); // open a GET request
xhr.send(); // send the request to the server.
```








المثال المذكور بالأعلي يقوم بإرسال طلب من نوع (GET request) الي [https://api.github.com/users/manishmshiva](https://api.github.com/users/manishmshiva) لإستدعاء بيانات صفحتي الشخصية من علي (Github) في صيغة (JSON).

إذا تحقق الطلب وكان ناجحا، سيتم طباعة الآتي في لوحة التحكم (console):

![5-2](https://www.freecodecamp.org/news/content/images/2020/08/5-2.png)

أما إذا فشل طلب الإستدعاء، سيتم طباعة رسالة الخطأ (error message) في لوحة التحكم كما هو موضح بالأسفل:

![8-1](https://www.freecodecamp.org/news/content/images/2020/08/8-1.png)


## طلب بإستخدام الـ(Fetch API)
يعتبر الـ(Fetch API) النسخة الاكثر سهولة وبساطة من دالة الـ(()XMLHttpRequest) من حيث الإستخدام. حيث يمكن من خلالها استهلاك الموارد واستدعاء البيانات بشكل متزامن (asynchronously). 

الإختلاف الأساسي بين الـ(fetch) والـ(()XMLHttpRequest) هو ان الـ(fetch API) يعمل من خلال العهود (Promises) وليس بإستخدام دوال الإسترجاع (callbacks) كما هو الحال مع الـ(()XMLHttpRequest). وهذا في حد ذاته له العديد من المميزات. علي سبيل المثال، في حال كان تطبيق الويب الذي تعمل عليه معقد وضخم فإنك الي حد كبير ستعاني معاناة شديدة إذا ما إستخدمت دوال الإسترجاع...وهذا الأمر شائع بشكل كبير لدرجة ان هناك مصطلحا قد ادرج تحت إسم "جحيم دوال الإسترجاع" ([callback hell](http://callbackhell.com/)).

علي العكس من ذلك، فإن إستخدام العهود (promises) يتميز ببساطة وسهولة كتابة طلبات التزامن (asynchronous requests). إذا أردت معرفة المزيد عن العهود وطرقة عملها وإستخدامها يمكن قراءة المقال علي [هذا الرابط](https://javascript.info/promise-basics). 

بإستخدام نفس المثال السابق، هكذا سيكون شكل تطبيق دالة الـ(fetch) مقارنة بدالة الـ(()XML HttpRequest)


```javascript
// GET Request.
fetch('https://api.github.com/users/manishmshiva')
    // Handle success
    .then(response => response.json())  // convert to json
    .then(json => console.log(json))    //print data to console
    .catch(err => console.log('Request Failed', err)); // Catch errors
```





المعامل الأول (first parameter) لدالة الـ(fetch) يجب ان يكون من نوع رابط (URL) دائماً...أما المعامل الثاني (second parameter) فهو إختياري (أي يمكنك إضافته إذا أردت ذلك أو في حالة عدم إضافته فلن يؤثر بالسلب علي تطبيق وأداء ونتيجة إستخدام الدالة)...وفي هذه الحالة يمكن إستخدام المعامل الثاني لتحديد نوع الطريقة (method) او توصيف رأس الطلب (headers). 


ولكن هناك إختلاف أساسي ما بين نوع الرد (response object) الذي ينتج عن إستخدام الـ(()XMLHttpRequest) مقارنة بالـ(fetch).

البيانات المستدعاه بإستخدام اـ(XMLHttpRequest) تأتي في صورة الرد ذاته (reponse object) أما الرد الناتج عن إستخدام (fetch) فيحتوي علي بيانات إضافية، مثل رأس الرد (response headers) وكود الحالة (status code). لذلك عند إستخدام (fetch) يستلزم ذلك إضافة او إلحاق طريقة (()json.) الي الرد للحصول علي البيانات المرغوبة والمحلقة بالرد بشكل صحيح (()res.json).

هناك أيضاً إختلاف أخر، وهو أن الـ(fetch) لن تُظهِر إذا ما كان هناك خطأ قد حدث إذا ما أرجع الرد كود حالة رقم 400 او 500، ولكن سيُعتمَد الرد علي انه ناجح بالفعل وسيتم إرساله الي الدالة التالية (()then.). 

إذاً متي تُظهِر دالة الـ(fetch) أن هناك خطأ؟ يحدث هذا فقط في حالة إذا ما تم إعتراض او قطع الطلب (request). لكي يتم التعامل مع هذا الخطأ، يمكنك إستخدام طريقة (()status.) علي الرد (response) ليصبح (()response.status) للإطلاع علي كود الحالة، والذي يكون كود 400 او 500 في تلك الحالة.

عظيم جداً. أنت الآن تفهم كيفية عمل الـ(Fetch API). دعونا الآن نتطلع إلي أمثلة أخري والتي تتضمن ادخال البيانات والعمل مع رأس الطلب (headers).


## طريقة التعامل مع رأس الطلب(Headers)
يمكن ادخال البيانات الي الطلب من خلال إدخال خاصية الـ(headers) كأحد المدخلات إلي دالة الـ(fetch) كما هو موضع فالمثال بالأسفل. يمكنك إستخدام دالة الإنشاء (constructor) الخاصة بالرأس ([headers constructor](https://developer.mozilla.org/en-US/docs/Web/API/Headers)). ويمكنك أيضاً إدخال مكون JSON (JSON object) مباشرة الي خاصية الرأس (header property) كبديل لإستخدام دالة الإنشاء (constructor)، والتي تنجح في أغلب الحالات.


```javascript
fetch('https://api.github.com/users/manishmshiva', {
  method: "GET",
  headers: {"Content-type": "application/json;charset=UTF-8"}
})
.then(response => response.json()) 
.then(json => console.log(json)); 
.catch(err => console.log(err));
```




## إدخال البيانات إلي طلب من نوع (POST Request)

في حالة الطلب من نوع (POST request) يمكنك إستخدام خاصية جسم الطلب (body property) لإرسال تسلسل من الحروف يطلق عليه (JSON string)...لاحظ ان هناك فرق ما بين نوع الـ(JSON) المستخدم لأرسال تسلسل الحروف بإستخدام خاصية جسم الطلب والذي هو من نوع (JSON string)، وبين نوع الـ(JSON) المستخدم في رأس الطلب (headers) وهو من نوع الـ(JSON object).


```javascript
// data to be sent to the POST request
let _data = {
  title: "foo",
  body: "bar", 
  userId:1
}

fetch('https://jsonplaceholder.typicode.com/posts', {
  method: "POST",
  body: JSON.stringify(_data),
  headers: {"Content-type": "application/json; charset=UTF-8"}
})
.then(response => response.json()) 
.then(json => console.log(json));
.catch(err => console.log(err));
```





يجب ملاحظة أن الـ(Fetch API) مازال في مرحلة التطوير ويمكننا توقع الحصول علي خصائص وإمكانيات أفضل في المستقبل القريب.

هذا لا يعني بالضرورة أنه لا يمكنك إستخدامه في تطوير مواقع وتطبيقات الويب الخاصة بك، حيث أن معظم المتصفحات تدعم إستخدام الـ(Fetch API). يمكنك إستخدام الجدول المرفق بالأسفل للتعرف علي تلك المتصفحات الداعمة لإستخدامه علي كلا من أجهزة الكمبيوتر الشخصية كالـ(PC) والابتوب وأجهزة الكمبيوتر المستخدمه في المكاتب والمنازل وكذلك أجهزة الهواتف المحمولة.

![6-2](https://www.freecodecamp.org/news/content/images/2020/08/6-2.png)

أتمني أن يكون هذا المقال قد ساعدك علي فهم وإستيعاب كيفية عمل وطريقة إستخدام الـ(Fetch API) بشكل مبسط واتمني أن تقوم بتجربة إستخدامه في تطبيقك القادم.

---
# *ORIGINAL article attached below, in case it is NOT available on freeCodeCamp anymore.*
---

# JavaScript Fetch API Tutorial with JS Fetch Post and Header Examples

By: [Manish Shivanandhan](https://www.freecodecamp.org/news/author/manishmshiva/)

*Translated by: [Ahmed E. F. R. Mohammed](https://github.com/AhmedEFRMElwazery)*

If you are writing a web application, chances are you will have to work with external data. This can be your own database, third party APIs, and so on.

When [AJAX](https://en.wikipedia.org/wiki/Ajax_%28programming%29) first appeared in 1999, it showed us a better way to build web applications. AJAX was a milestone in web development and is the core concept behind many modern technologies like React.

Before AJAX, you had to re-render an entire web page even for minor updates. But AJAX gave us a way to fetch content from the backend and update selected user interface elements. This helped developers improve user experience and build larger, complicated web platforms.

## Crash Course on REST APIs

![1-9](https://www.freecodecamp.org/news/content/images/2020/08/1-9.png)

We are now in the age of [RESTful APIs](https://restfulapi.net/). Simply put, a REST API lets you push and pull data from a datastore. This might either be your database or a third party’s server like the [Twitter API](https://developer.twitter.com/en/docs/twitter-api).

There are a few different types of REST APIs. Let’s look at the ones you will use in most cases.

-   **GET** — Get data from the API. For example, get a twitter user based on their username.
-   **POST** — Push data to the API. For example, create a new user record with name, age, and email address.
-   **PUT** — Update an existing record with new data. For example, update a user’s email address.
-   **DELETE** — Remove a record. For example, delete a user from the database.

There are three elements in every REST API. The request, response, and headers.

**Request** — This is the data you send to the API, like an order id to fetch the order details.

![2-6](https://www.freecodecamp.org/news/content/images/2020/08/2-6.png)Sample Request

**Response** — Any data you get back from the server after a successful / failed request.

![3-5](https://www.freecodecamp.org/news/content/images/2020/08/3-5.png)

Sample Response

**Headers** — Additional metadata passed to the API to help the server understand what type of request it is dealing with, for example “content-type”.

![4-2](https://www.freecodecamp.org/news/content/images/2020/08/4-2.png)

Sample Headers

The real advantage of using a REST API is that you can build a single API layer for multiple applications to work with.

If you have a database that you want to manage using a web, mobile, and desktop application, all you need is a single REST API Layer.

Now that you know how REST APIs work, let's look at how we can consume them.

## XMLHttpRequest

Before [JSON](https://www.w3schools.com/js/js_json_intro.asp) took over the world, the primary format of data exchange was XML. XMLHttpRequest() is a JavaScript function that made it possible to fetch data from APIs that returned XML data.

XMLHttpRequest gave us the option to fetch XML data from the backend without reloading the entire page.

This function has grown from its initial days of being XML only. Now it supports other data formats like JSON and plaintext.

Let's write a simple XMLHttpRequest call to the GitHub API to fetch my profile.

```javascript
// function to handle success
function success() {
    var data = JSON.parse(this.responseText); //parse the string to JSON
    console.log(data);
}

// function to handle error
function error(err) {
    console.log('Request Failed', err); //error details will be in the "err" object
}

var xhr = new XMLHttpRequest(); //invoke a new instance of the XMLHttpRequest
xhr.onload = success; // call success function if request is successful
xhr.onerror = error;  // call error function if request failed
xhr.open('GET', 'https://api.github.com/users/manishmshiva'); // open a GET request
xhr.send(); // send the request to the server.
```

The above code will send a GET request to [https://api.github.com/users/manishmshiva](https://api.github.com/users/manishmshiva) to fetch my GitHub info in JSON. If the response was successful, it will print the following JSON to the console:

![5-2](https://www.freecodecamp.org/news/content/images/2020/08/5-2.png)

If the request failed, it will print this error message to the console:

![8-1](https://www.freecodecamp.org/news/content/images/2020/08/8-1.png)

## Fetch API

The Fetch API is a simpler, easy-to-use version of XMLHttpRequest to consume resources asynchronously. Fetch lets you work with REST APIs with additional options like caching data, reading streaming responses, and more.

The major difference is that Fetch works with promises, not callbacks. JavaScript developers have been moving away from callbacks after the introduction of promises.

For a complex application, you might easily get into a habit of writing callbacks leading to [callback hell](http://callbackhell.com/).

With promises, it is easy to write and handle asynchronous requests. If you are new to promises, [you can learn how they work here](https://javascript.info/promise-basics).

Here is how the function we wrote earlier would look like if you used fetch() instead of XMLHttpRequest:

```javascript
// GET Request.
fetch('https://api.github.com/users/manishmshiva')
    // Handle success
    .then(response => response.json())  // convert to json
    .then(json => console.log(json))    //print data to console
    .catch(err => console.log('Request Failed', err)); // Catch errors
```

The first parameter of the Fetch function should always be the URL. Fetch then takes a second JSON object with options like method, headers, request body, and so on.

There is an important difference between the response object in XMLHttpRequest and Fetch.

XMLHttpRequest returns the data as a response while the response object from Fetch contains information about the response object itself. This includes headers, status code, etc. We call the “res.json()” function to get the data we need from the response object.

Another important difference is that the Fetch API will not throw an error if the request returns a 400 or 500 status code. It will still be marked as a successful response and passed to the ‘then’ function.

Fetch only throws an error if the request itself is interrupted. To handle 400 and 500 responses, you can write custom logic using ‘response.status’. The ‘status’ property will give you the status code of the returned response.

Great. Now that you understand how the Fetch API works, let's look at a couple more examples like passing data and working with headers.

## Working with Headers

You can pass headers using the “headers” property. You can also use the [headers constructor](https://developer.mozilla.org/en-US/docs/Web/API/Headers) to better structure your code. But passing a JSON object to the “headers” property should work for most cases.

```javascript
fetch('https://api.github.com/users/manishmshiva', {
  method: "GET",
  headers: {"Content-type": "application/json;charset=UTF-8"}
})
.then(response => response.json()) 
.then(json => console.log(json)); 
.catch(err => console.log(err));
```

## Passing Data to a POST Request

For a POST request, you can use the “body” property to pass a JSON string as input. Do note that the request body should be a JSON string while the headers should be a JSON object.

```javascript
// data to be sent to the POST request
let _data = {
  title: "foo",
  body: "bar", 
  userId:1
}

fetch('https://jsonplaceholder.typicode.com/posts', {
  method: "POST",
  body: JSON.stringify(_data),
  headers: {"Content-type": "application/json; charset=UTF-8"}
})
.then(response => response.json()) 
.then(json => console.log(json));
.catch(err => console.log(err));
```

The Fetch API is still in active development. We can expect better features in the near future.

However, most browsers support the use of Fetch in your applications. The chart below should help you figure out which browsers support it on the web and mobile apps.

![6-2](https://www.freecodecamp.org/news/content/images/2020/08/6-2.png)

I hope this article helped you understand how to work with the Fetch API. Be sure to try out Fetch for your next web application.
