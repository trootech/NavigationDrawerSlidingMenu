[![](https://jitpack.io/v/trootech/NavigationDrawerSlidingMenu.svg)](https://jitpack.io/#trootech/NavigationDrawerSlidingMenu)
[![API](https://img.shields.io/badge/API-21%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=21)

# Navigation drawer slider
Create custom navigation drawer with good animation. This is really good navigation slider drawer.

## Setup
```gradle
//project label build.gradle
buildscript {
    repositories {
         ....
        maven { url 'https://jitpack.io' }
    }
}

allprojects {
    repositories {
     .......
        maven { url 'https://www.jitpack.io' }
    }
}
//app label build.gradle
dependencies {
    implementation 'com.github.trootech:NavigationDrawerSlidingMenu:1.0.0'
}
```

## Result Demo:

<img src="https://user-images.githubusercontent.com/112152331/187843772-d3a519e4-b337-4826-b3a3-7d07d4bbd172.gif" width="300" />

## Usage
- Create menu.xml under your res/layout/drawer_menu
  Create slide menu view view details regarding UI.
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/white"
    android:orientation="vertical">
  
    <Space
        android:layout_width="wrap_content"
        android:layout_height="56dp" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/list"
        android:layout_width="240dp"
        android:layout_height="wrap_content" />

    <Space
        android:layout_width="wrap_content"
        android:layout_height="40dp" />

</LinearLayout>
```

* Set the content view (for example, using setContentView in your activity).
* Create your array.xml (example) or construct a View programmatically. Under array.xml set title and drawer image.

-Initialization root view and access all filed.
```
//Interface through root view managed. Like Drawer open/closed/layout etc managed.
private var slidingRootNav: DrawerSlidingRootNav? = null
slidingRootNav =  DrawerRootNavBuilder(this)
                .withToolbarMenuToggle(toolbar)
                .withSavedState(savedInstanceState)
                .withMenuLayout(R.layout.drawer_menu)
                .inject();
```

| Syntax                                   | Description                                                                            |
| -----------------------------            | -----------                                                                            |
| withMenuOpened(false)                    | Initial menu opened/closed state. Default == true                                      |
| withContentClickableWhenMenuOpened(true) | If true, a user can't open or close the menu. Default == true                          |
| withGravity(SlideGravity.LEFT)           | If LEFT you can swipe a menu from left to right, if RIGHT - the direction is opposite. |

# Initial menu opened/closed state.
-withContentClickableWhenMenuOpened = false

<img src="https://user-images.githubusercontent.com/112152331/187609875-f1d27e3f-581f-4ef5-84b1-4c61d214d465.gif" width="300" />


-Controlling the layout using Interface
```
public interface SlidingRootNav {
    boolean isMenuClosed();
    boolean isMenuOpened();
    boolean isMenuLocked();
    void closeMenu();
    void closeMenu(boolean animated);
    void openMenu();
    void openMenu(boolean animated);
    void setMenuLocked(boolean locked);
    SlidingRootNavLayout getLayout(); //If for some reason you need to work directly with layout - you can
}
```

-Slide menu required list item add
```
 val arrayList = listOf(
            createItemFor(POS_DASHBOARD),
            createItemFor(POS_ACCOUNT),
            createItemFor(POS_MESSAGES),
            createItemFor(POS_CART),
            SpaceItem(48),
            createItemFor(POS_LOGOUT)
        )
        val adapter = DrawerAdapter(arrayList)
        //If need to first time initialization Time show any position default selected. so, that time this item position pass instance of POS_DASHBOARD.
        adapter.setSelected(POS_DASHBOARD)
              
```


