---
layout: post
title: "linear layout demo"
description: "linear layout demo"
tags: [development]
published: true
---
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >
    <EditText 
        android:id="@+id/editText1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="UserName"/>
    <EditText 
        android:id="@+id/editText2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="textPassword"/>
    <Button 
        android:id="@+id/button1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button"/>
    <LinearLayout 
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        >
        
    <TextView 
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Gender"
        android:textAppearance="?android:attr/textAppearanceMedium"/>
    <RadioButton 
        android:id="@+id/radioButton01"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Male" />
    <RadioButton 
        android:id="@+id/radioButton02"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Female" />    
    
</LinearLayout>
</LinearLayout>