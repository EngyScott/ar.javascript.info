**خطأ**!

حاول هذا:

```js run
let user = {
  name: "John",
  go: function() { alert(this.name) }
}

(user.go)() // خطأ!
```

لا تعطينا رسالة الخطأ في معظم المتصفحات الكثير من الأدلة حول الخطأ الذي حدث.

**يظهر الخطأ لأن فاصلة منقوطة مفقودة بعد `user = {...}`.**

لا تقوم جافاسكريبت بإدراج فاصلة منقوطة تلقائيًا قبل قوس `()(user.go)`, إنها تقوم بقراءة الشيفرة هكذا:

```js no-beautify
let user = { go:... }(user.go)()
```

ثم يمكننا أن نرى أيضًا أن هذا التعبير المشترك هو عبارة عن استدعاء للكائن `{ go: ... }` كتابع مع متغير `(user.go)`. وهذا يحدث أيضًا على نفس السطر مع `let user`, لذلك `user` لم يتم حتى الآن تعريف الكائن ، ومن هنا كان الخطأ.

إذا أدخلنا الفاصلة المنقوطة ، فكل شيء على ما يرام:

```js run
let user = {
  name: "John",
  go: function() { alert(this.name) }
}*!*;*/!*

(user.go)() // John
```

يرجى ملاحظة أن الأقواس حول `(user.go)` لا تفعل شيئ هنا.عادة ما يقومون بإعداد ترتيب العمليات ، ولكن هنا النقطة
 `.` تعمل أولاً على أي حال, لذلك ليس هناك تأثير. فقط الشيء الفاصلة المنقوطة هو المهم.
