#### NavigationGraph_Demo

It simplifies the implementation of the navigation in an Android app, it helps with implementing the navigation between your app destinations.

It was designed with a Single Activity App concept in mind and is defined by 3 main components:

- A Navigation Graph: a file containing a set of destinations and respective actions, defining a navigation architecture for the app. An app can have one or more navigation graphs or sub-graphs.
- Destination: a destination on the app, usually a fragment, but a destination can also be an Activity, another navigation graph or sub-graph, and custom destination types are also supported.
- Action: the connections between the app destinations.

### Demo

<img src="https://user-images.githubusercontent.com/10658016/71170500-6fcc3180-2281-11ea-9b80-79a569a07e6d.gif?raw=true" alt="Home Page" width="300"/>
</p>

#### Code Setup
```
def nav_version = "2.1.0"

dependencies {
    // Kotlin
    implementation "androidx.navigation:navigation-fragment-ktx:$nav_version"
    implementation "androidx.navigation:navigation-ui-ktx:$nav_version"
}

```
navgraph.xml

```
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/nav_graph"
    app:startDestination="@id/main_fragment">

    <fragment
        android:id="@+id/main_fragment"
        android:name="com.example.navigationgraph_demo.MainFragment"
        android:label="MainFragment"
        tools:layout="@layout/main_fragment">
        <action
            android:id="@+id/fragmentMainToFirst"
            app:destination="@+id/firstFragment" />
    </fragment>
    <fragment
        android:id="@+id/firstFragment"
        android:name="com.example.navigationgraph_demo.FirstFragment"
        android:label="MainFragment"
        tools:layout="@layout/first_fragment">
        <action
            android:id="@+id/fragmentFirstToSecond"
            app:destination="@+id/secondFragment" />
    </fragment>

    <fragment
        android:id="@+id/secondFragment"
        android:name="com.example.navigationgraph_demo.SecondFragment"
        android:label="MainFragment"
        tools:layout="@layout/second_fragment">
        <action
            android:id="@+id/fragmentSecondToThird"
            app:destination="@id/thirdFragment" />
    </fragment>

    <fragment
        android:id="@+id/thirdFragment"
        android:name="com.example.navigationgraph_demo.ThirdFragment"
        android:label="MainFragment"
        tools:layout="@layout/third_fragment">

    </fragment>
</navigation>
```

main_activity.xml

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".HomeActivity">

    <fragment
        android:id="@+id/nav_host_fragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        app:defaultNavHost="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:navGraph="@navigation/nav_graph" />


</LinearLayout>
```

How to navigate?

```
 view.findViewById<Button>(R.id.button).setOnClickListener {

            view.findNavController().navigate(R.id.fragmentMainToFirst)
        }
```
