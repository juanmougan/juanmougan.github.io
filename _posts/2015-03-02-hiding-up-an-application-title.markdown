---
layout: post
title:  "Hiding an Application's title in Android 4"
date:   2015-03-02 16:13:00
categories: Development Java Android
---
I was trying to hide an application's title from the Action bar. The first possible approach was a nasty hack: just setting the label to an empty string, like this

{% highlight xml %}
android:label=""
{% endhighlight %}

in the Manifest. However, choosing this approach leads you into two problems:

1. The application's name, below the icon, will be blank

2. You won't see the app in the "recent apps" list

Googling (for some time) led my to [this StackOverflow's answer](http://stackoverflow.com/a/14313108/3923525). It's basically what we are looking for, with just a tiny adjustment: we are going to remove the ActionBarSherlock part, since we are using Android 4.0+. So, in the `styles.xml` file, the code will look like this:

{% highlight xml %}
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="actionBarStyle">@style/Widget.Styled.ActionBar</item>
        <item name="android:actionBarStyle">@style/Widget.Styled.ActionBar</item>
    </style>

    <style name="Widget.Styled.ActionBar" parent="Widget.AppCompat.Light.ActionBar.Solid.Inverse">
        <item name="android:displayOptions">showHome|useLogo</item>
        <item name="displayOptions">showHome|useLogo</item>
    </style>

</resources>
{% endhighlight %}

Of course, our new style needs to be referenced from the Manifest, like this:

{% highlight xml %}
<application
    android:allowBackup="true"
    android:icon="@drawable/icon"
    android:label="@string/app_name"
    android:theme="@style/AppTheme">
    ...
{% endhighlight %}

That's it! Hope you'll find it useful
