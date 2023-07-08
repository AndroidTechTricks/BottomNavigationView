# BottomNavigationView

## **Step : 1 -** Create Menu Items
- create **menu** package inside **res** package and by right clicking on menu create new .xml file named **"bottom_navigation_item.xml'**. By creating this you have to paste below code for creating 4 items as menu.
- Provide icon and title according to your requirement for each item.
- 
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/navigation_home"
        android:title="@string/home_label"
        android:icon="@drawable/baseline_home_24"/>

    <item android:id="@+id/navigation_fav"
        android:title="@string/fav_label"
        android:icon="@drawable/baseline_favorite_border_24"/>

    <item android:id="@+id/navigation_search"
        android:title="@string/search_label"
        android:icon="@drawable/baseline_search_24"/>

    <item android:id="@+id/navigation_profile"
        android:title="@string/profile_label"
        android:icon="@drawable/baseline_person_24"/>
</menu>

## **Step : 2 -** Create Nav-Graph
### Nav-Graph is mandatory for creating actions on click of menu items
- Create package named **'navigation'** under **res** package,
  Then create .xml file by right click on navigation named as **'mobile_navigation.xml'**.
- Navigation-Graph also handles the transactions from one fragment to another fragment for smaller projects, but if you are creating large scale project use custom
  handling for nav-graph.
- **Now, You have to create 4 fragments e.g - HomeFragment, FavouriteFragment, SearchFragment, ProfileFragment etc.**
- Here, We have created the basic structure of nav-graph like below:

<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/mobile_navigation"
    app:startDestination="@+id/navigation_home">

    <fragment
        android:id="@+id/navigation_home"
        android:name="com.example.androidtechtricks.home.HomeFragment"
        android:label="@string/home_label"
        tools:layout="@layout/fragment_home" />

    <fragment
        android:id="@+id/navigation_fav"
        android:name="com.example.androidtechtricks.favourite.FavouriteFragment"
        android:label="@string/fav_label"
        tools:layout="@layout/fragment_favourite" />

    <fragment
        android:id="@+id/navigation_search"
        android:name="com.example.androidtechtricks.search.SearchFragment"
        android:label="@string/search_label"
        tools:layout="@layout/fragment_search" />

    <fragment
        android:id="@+id/navigation_profile"
        android:name="com.example.androidtechtricks.profile.ProfileFragment"
        android:label="@string/profile_label"
        tools:layout="@layout/fragment_profile" />

</navigation>

## **Step : 3 -** Structure **activity_main.xml** like below

    <?xml version="1.0" encoding="utf-8"?>
    <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

    <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottomnavigation"
        android:layout_width="@dimen/space_0"
        android:layout_height="wrap_content"
        android:layout_marginHorizontal="@dimen/space_12"
        android:layout_marginBottom="@dimen/space_16"
        android:background="@drawable/bottom_navigation_bg"
        android:padding="@dimen/space_8"
        app:elevation="@dimen/space_8"
        app:itemBackground="@drawable/item_bg"
        app:itemHorizontalTranslationEnabled="true"
        app:labelVisibilityMode="unlabeled"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:menu="@menu/bottom_navigation_item" />

    <fragment
        android:id="@+id/nav_host_fragment_activity_main"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:defaultNavHost="true"
        app:layout_constraintBottom_toTopOf="@id/bottomnavigation"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:navGraph="@navigation/mobile_navigation" />

    </androidx.constraintlayout.widget.ConstraintLayout>

## **Step : 4 -** In **MainActivity.kt** activity file attach navigation-controller to handle fragments transaction 
- Attach NavController to the fragment e.g - nav_host_fragment_activity_main to controller clicks on bottom menu items and open fragment respective fragment on screen.

       private lateinit var navController: NavController
       
       navController = findNavController(R.id.nav_host_fragment_activity_main)

       val appBarConfiguration = AppBarConfiguration(
           setOf(
                    R.id.navigation_home,
                    R.id.navigation_fav,
                    R.id.navigation_search,
                    R.id.navigation_profile
                )
            )
         
        setupActionBarWithNavController(navController, appBarConfiguration)
        binding.bottomnavigation.setupWithNavController(navController)
