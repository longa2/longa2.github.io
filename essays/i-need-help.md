---
layout: essay
type: essay
title: "I Need Help!"
# All dates must be YYYY-MM-DD format!
date: 2025-09-11
published: true
labels:
  - Software Engineering
  - Stack Overflow
  - Questions
---

<img width="200px" class="rounded float-start pe-4" src="../img/i-need-help-quote.jpg">

*"Never underestimate the power of stupid people in large groups." ~ George Carlin*

## Any Questions?

Questions have always been a long-standing way of searching for answers to the problems around us in day-to-day life. So what happens when you ask one? Do you get an answer as expected? In some cases, sure you can. But, in other cases, there are questions unanswered - or better yet - there already is an answer and no one is bothered to answer it for you.

## The Wrong Way

When someone asks a question, they are seeking a solution. Ususally, it is so. But sometimes, people ask not to seek a solution to a problem, but rather in redundancy. Take for example this user:

### Question

In the example below, childOfNumbers is correctly inferred to be Child<number>. However, my issue is childOfStrings is inferred to be Base<string>. Is it possible to have a parent return the subclasses type such that childOfStrings is inferred to being Child<string>?

Code
```
abstract class Base<T> {
    public items: T[] = []
    constructor(items: T[] =[]) {
        this.items = items;
    }
    abstract createInstance<U>(args: U[]): Base<U>;
    map<U>(fn: (value: T, index: number) => U): Base<U> {
        return this.createInstance(this.items.map((v, i) => fn(v,i)))
    }
}

class Child<T> extends Base<T> {
    override createInstance<U>(args: U[]): Base<U> {
        return new Child(args)
    }
}

const childOfNumbers = new Child<number>([1,2,3]);
const childOfStrings = childOfNumbers.map((v,i) => v.toString())
```
[Source](https://stackoverflow.com/questions/79762418/return-subclass-type-from-parent-function)

The question posed above seems to be a fair question, no? However, why is it that no one responded to this post - let alone an answer to the problem? The reason is that the user did not show to be an individual who is willing to learn. Rather, the context provided by the user shows that they ran into a problem and wants to know the solution with no attempt in finding the answer themselves. Simply put, this is tantamount to laziness. As such, no reply was ever made despite the significant number of online users that had viewed it and could have easily provided an answer.

## The Right Way

Let's take a look at another user's question:

### Talk to my Android app directly using Google Assistant to complete a easy task

I have created simple app to integrate the Google Assistant which is named as TestAppDemo. I have added simple screen where I have one edittext where I am entering the random things like groceries or anything we can add as per our convenience. I want to say to google *"Hey Google, Open groceries from TestAppDemo" *

I have created Simple MainActivity which uses the ShortcutHelper class

```
shortcutHelper = ShortcutHelper(this)

        binding.btnCreateShortcut.setOnClickListener {
            val itemName = binding.inputItem.text.toString().trim()
            if (itemName.isNotEmpty()) {
                shortcutHelper.pushDynamicShortcut(itemName)
                Toast.makeText(this, "Shortcut created for \"$itemName\"", Toast.LENGTH_SHORT).show()
                binding.inputItem.text.clear()
            } else {
                Toast.makeText(this, "Please enter an item name", Toast.LENGTH_SHORT).show()
            }
        }

        // If started via shortcut, display incoming "item" parameter
        intent.getStringExtra("item")?.let { item ->
            Toast.makeText(this, "Opened via shortcut for item: \"$item\"", Toast.LENGTH_LONG).show()
        }
```

In My ShortcutHelper

```
fun pushDynamicShortcut(itemName: String) {
        val shortcutId = "shortcut_$itemName"

        val intent = Intent(context, MainActivity::class.java).apply {
            action = Intent.ACTION_VIEW
            putExtra("item", itemName)
        }

        val shortcut = ShortcutInfoCompat.Builder(context, shortcutId)
            .setShortLabel(itemName)
            .setLongLabel("Open \"$itemName\" from TestAppDemo")
            .addCapabilityBinding(
                "actions.intent.GET_THING",
                "thing.name",
                listOf(itemName)
            )
            .setIntent(intent)
            .build()

        ShortcutManagerCompat.pushDynamicShortcut(context, shortcut)
    }
```

Also created Shortcut to use capabilities

```
 <capability android:name="actions.intent.GET_THING">
        <intent
            android:action="android.intent.action.VIEW"
            android:targetPackage="com.example.testappdemo"
            android:targetClass="com.example.testappdemo.MainActivity">
            <parameter android:name="thing.name"
                android:key="item" />
        </intent>
    </capability>
```

In Manifest file

```
<meta-data
            android:name="android.app.shortcuts"
            android:resource="@xml/shortcuts" />
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
```

To achieve this I have used BII (Build In Intent) which is * "actions.intent.GET_THING"* to develop a demo, but that was also not producing the desired results. For example, we could just say "Hey Google, Open groceries from TestAppDemo" to open the task, but it's not opening that screen in the app or I can say it's not giving the output

So my question is, is it possible to directly interact with my app and have it do a very simple task?

Expectation: When I say to google assistant "Hey Google, Open groceries from TestAppDemo" it should navigate to particular groceries screen

Actual :When I say to google assistant "Hey Google, Open groceries from TestAppDemo" it is not navigating to the groceries screen

[Source](https://stackoverflow.com/questions/79762517/talk-to-my-android-app-directly-using-google-assistant-to-complete-a-easy-task)

Despite being posted the same day as the previous post, this user has already garnered a reply answer. This indicates that with proper context and a properly-phrased question gives way for more clarity in the problem and thus would draw more people to answer.

## Conclusion

The juxtaposition is clear to see in both users' posts. The former, albeit with an honest question, asks a question in regards to a fundamental concept of classes. The latter, however, provides not only detailed context of what their problem is, but also indicates that their expectation was not the result they had hoped to achieve. In general, asking questions is always a sign of wanting to learn, solve, and overcome the many challenges in life. However, especially in this era of widely-available information on the internet, there needs to be a clear and concise intention in solving the problem - otherwise, people that are more knowledgeable and intelligent than you are will not give you and your issue the light of day.
