# Android Developer Fundamentals — Exhaustive Exam-Ready Notes
## Pages 5–280 | Complete Coverage

---

# CHAPTER 1.0: Introduction to Android

## Concept Overview
Android is an **operating system and programming platform** developed by Google for smartphones and other mobile devices such as tablets. It runs on many different devices from many different manufacturers. Android includes:
- A **software development kit (SDK)** for writing original code and assembling software modules
- A **marketplace** to distribute apps (Google Play)
- An entire **ecosystem** for mobile apps

**Mental model:** Think of Android as a layered cake. From bottom up: Linux Kernel → Hardware Abstraction Layer → Android Runtime + Libraries → Java API Framework → Apps.

---

## Theory & Logic

### Why Develop for Android?
- World's most popular mobile platform, powering hundreds of millions of devices in 190+ countries
- Largest installed base of any mobile platform, still growing fast
- Every day another million users power up their Android devices for the first time

### Best Experience for App Users
- Touch-screen UI based on **direct manipulation** (swiping, tapping, pinching)
- Customizable virtual keyboard; supports game controllers and physical keyboards (Bluetooth/USB)
- Home screen: app icons + **widgets** (live, auto-updating content)
- Sensors: accelerometers, gyroscopes, proximity sensors for additional user actions
- **Haptic feedback** via vibration
- Built on **Linux kernel** — designed for battery-powered devices

### The Android Stack (Bottom-Up)

```
+------------------------------------------+
|            APPS (Your app, system apps)   |
+------------------------------------------+
|        JAVA API FRAMEWORK                 |
|  (View System, Resource Manager,          |
|   Notification Manager, Activity Manager, |
|   Content Providers)                      |
+------------------------------------------+
|  NATIVE C/C++ LIBRARIES  |  ANDROID      |
|  (OpenGL ES, SQLite, etc)|  RUNTIME (ART)|
+------------------------------------------+
|     HARDWARE ABSTRACTION LAYER (HAL)      |
|  (Camera module, Bluetooth module, etc.)  |
+------------------------------------------+
|             LINUX KERNEL                  |
|  (Threading, Low-level memory mgmt,       |
|   Device drivers, Security)               |
+------------------------------------------+
```

**Layer explanations:**
1. **Apps**: Your apps + core system apps (email, SMS, calendar, browser, contacts)
2. **Java API Framework**: All Android features exposed through Java APIs
   - **View System**: builds UI (lists, buttons, menus)
   - **Resource Manager**: accesses localized strings, graphics, layouts
   - **Notification Manager**: displays custom alerts in status bar
   - **Activity Manager**: manages app lifecycle
   - **Content Providers**: enables apps to access data from other apps
3. **Libraries & Android Runtime (ART)**: Each app runs in its own process with its own ART instance. ART enables multiple VMs on low-memory devices. Includes core runtime libraries.
4. **Hardware Abstraction Layer (HAL)**: Standard interfaces exposing hardware capabilities to higher-level Java API. Each hardware type (camera, Bluetooth) = one library module.
5. **Linux Kernel**: Foundation of the platform. Used for threading, low-level memory management, device drivers, and security features.

### Distribution Options
- Email, website, or **Google Play** marketplace
- Google Play = official appstore for Android; billions of downloads monthly

### Android Versions Table

| Code Name        | Version     | API Level |
|-----------------|-------------|-----------|
| (N/A)           | 1.0         | 1         |
| Cupcake         | 1.5         | 3         |
| Donut           | 1.6         | 4         |
| Eclair          | 2.0–2.1     | 5–7       |
| Froyo           | 2.2–2.2.3   | 8         |
| Gingerbread     | 2.3–2.3.7   | 9–10      |
| Honeycomb       | 3.0–3.2.6   | 11–13     |
| Ice Cream Sandwich | 4.0–4.0.4 | 14–15    |
| Jelly Bean      | 4.1–4.3.1   | 16–18     |
| KitKat          | 4.4–4.4.4   | 19–20     |
| Lollipop        | 5.0–5.1.1   | 21–22     |
| Marshmallow     | 6.0–6.0.1   | 23        |
| Nougat          | 7.0         | 24        |

**Best practice**: Support ~90% of active devices while targeting the latest version. Use the Android Support Library to enable recent APIs on older devices.

### Challenges of Android App Development
1. **Multi-screen world**: Different form factors, sizes, manufacturers' custom UI elements
2. **Performance**: Battery life, multimedia content, network access all affect performance
3. **Security**: Use ProGuard to strip unused code; secure communication channels; protect user data
4. **Backward compatibility**: Must run on older API versions
5. **Market understanding**: Know your users

---

## Common Exam Traps / Edge Cases
- Android is based on **Linux kernel** — not the full Linux OS
- ART (Android Runtime) — **each app runs in its own process** with its own ART instance
- **HAL** is what shields the Java API Framework from hardware-specific details
- Minimum SDK vs Target SDK — these are different things (covered in 1.1)
- **WebP** format preferred over PNG/JPG for images

---

## Quick Revision Bullets
- Android = OS + SDK + marketplace ecosystem by Google, based on Linux kernel
- Five-layer stack: Apps → Java API Framework → Libraries+Runtime → HAL → Linux Kernel
- Google Play is the official app distribution channel; billions of downloads monthly
- API Level maps to each Android version (e.g., Nougat 7.0 = API 24)
- Best practice: support 90% of active devices; use Support Library for backward compat
- Four key development challenges: multi-screen, performance, security, backward compatibility

---
---

# CHAPTER 1.1: Create Your First Android App

## Concept Overview
This chapter covers the Android Studio IDE and the complete development workflow: from creating a project to running it on a device or emulator. Android Studio is the official IDE for Android development.

**Mental model:** Think of the development process as a pipeline: Idea → Design → Develop (Layout + Code + Manifest + Build) → Test → Publish.

---

## Theory & Logic

### The Development Process (Steps)
1. **Define the idea and requirements** — market and user research
2. **Prototype the UI** — drawings, mockups
3. **Develop and test** for each activity:
   - Create the layout (XML)
   - Write Java code
   - Register activity in manifest
   - Define the build
4. **Publish** — assemble the APK, distribute via Google Play

### Starting an Android Studio Project
- **Company Domain** → becomes the **package name** (must be unique for Play Store)
- Package name cannot be easily changed after publication
- **Minimum SDK** → minimum Android version your app supports
  - e.g., API 15 (Ice Cream Sandwich) = compatible with 97% of Play Store devices
- **Template** → Android Studio pre-populates code; Empty Activity is simplest

### Android Studio Window Panes

```
+----------------------------------------------------------+
|  TOOLBAR (Run, Debug, AVD, etc.)                         |
+----------------------------------------------------------+
| PROJECT   |    EDITOR PANE                  | PROPERTIES |
| PANE      |    (Java / XML / Layout Editor) |  PANE      |
|           |                                 |            |
+-----------+----------------------------------+-----------+
|  STATUS BAR (build progress, warnings)                   |
+----------------------------------------------------------+
| MONITOR PANE (Logcat, Android Monitor, TODO, Terminal)   |
+----------------------------------------------------------+
```

1. **Toolbar** — run app, launch Android tools
2. **Navigation Bar** — navigate project, open files
3. **Editor Pane** — edit selected file (code or layout)
4. **Status Bar** — project/IDE status, warnings
5. **Project Pane** — file hierarchy
6. **Monitor Pane** — logcat, Android Monitor, TODO, Terminal

### Exploring a Project (Android View)
- **AndroidManifest.xml** — app info for Android runtime
- **java/** — activities, tests, other Java components
- **res/** — layouts (XML), strings, images
- **build.gradle (Module: app)** — build config (minSdkVersion, targetSdkVersion, dependencies)

### The Android Manifest

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.android.helloworld">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme">

        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

**Key manifest attributes:**
- `android:allowBackup="true"` → automatic backup to cloud for API 23+
- `android:icon` → app icon from mipmap folder
- `android:label` → app name (use string resource `@string/app_name`)
- `android:theme` → UI theme (`@style/AppTheme`)
- `<uses-sdk android:minSdkVersion="14" android:targetSdkVersion="19" />` → API levels

**CRITICAL**: `targetSdkVersion` does NOT prevent app from running on newer Android versions. It tells the system whether the app should inherit new-version behavior changes.

### MainActivity.java — Skeleton

```java
// Every activity is a Java class that extends AppCompatActivity
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState); // always call super first
        setContentView(R.layout.activity_main); // inflate layout
    }
}
```

- **AppCompatActivity** = subclass of Activity that enables modern features + backward compatibility
- **onCreate()** = required callback, called when activity is first created
- **setContentView(R.layout.activity_main)** = inflates the XML layout

### Understanding build.gradle (Module: app)

```groovy
apply plugin: 'com.android.application'

android {
    compileSdkVersion 24           // compile against this SDK
    buildToolsVersion "24.0.1"    // build tools version

    defaultConfig {
        applicationId "com.example.android.helloworld"
        minSdkVersion 15           // minimum supported Android version
        targetSdkVersion 24        // highest optimized version
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])   // all .jar files in libs/
    compile 'com.android.support:appcompat-v7:24.2.1'   // AppCompat support library
    testCompile 'junit:junit:4.12'                       // unit testing
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
}
```

**Key points:**
- `minSdkVersion` and `targetSdkVersion` in `build.gradle` **override** any settings in AndroidManifest.xml
- Gradle uses **Groovy DSL** (Domain Specific Language)
- After changing build.gradle, always **Sync Now**
- `compile fileTree(dir: 'libs', include: ['*.jar'])` adds all .jar files in libs/ to the compilation classpath

### Running the App

**On Emulator (AVD):**
1. AVD Manager (Tools > Android > AVD Manager) → Create Virtual Device
2. Choose device definition (screen size, resolution, density)
3. Choose system image (Android version)
4. Run > Run app → select AVD → OK
5. Tip: Start emulator once per session, don't close it

**On Physical Device:**
1. Enable USB Debugging: Settings → About Phone → tap **Build Number 7 times** → Developer Options → USB Debugging
2. Connect via USB
3. Run > Run app → select device

**Troubleshooting connection:**
- Disconnect/reconnect device
- Restart Android Studio
- Revoke USB Debugging authorizations and re-grant

### Using the Log

```java
// Define log tag as a constant (best practice)
private static final String LOG_TAG = MainActivity.class.getSimpleName();

// Log levels:
Log.d(LOG_TAG, "Hello World");   // Debug
Log.e(LOG_TAG, "Error occurred"); // Error
Log.w(LOG_TAG, "Warning!");       // Warning
Log.i(LOG_TAG, "Info message");   // Info
Log.v(LOG_TAG, "Verbose");        // Verbose
```

**Log levels** (from least to most verbose): ERROR → WARN → INFO → DEBUG → VERBOSE

In Android Monitor's logcat tab, filter by level using the dropdown. Default is **Verbose** (shows all).

---

## Code: Complete HelloWorld Activity

```java
package com.example.android.helloworld;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;

public class MainActivity extends AppCompatActivity {

    // Best practice: define log tag as a constant
    private static final String LOG_TAG = MainActivity.class.getSimpleName();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);  // Always call super first
        setContentView(R.layout.activity_main); // Inflate the XML layout

        // Log a debug message — visible in logcat under DEBUG level
        Log.d(LOG_TAG, "Hello World");
    }
}
```

**Explanation:**
- `super.onCreate(savedInstanceState)` — required; sets up the base Activity
- `setContentView(R.layout.activity_main)` — links to `res/layout/activity_main.xml`
- `Log.d(LOG_TAG, "Hello World")` — logs to Android Monitor (logcat)

---

## Common Exam Traps / Edge Cases
- `minSdkVersion` ≠ `targetSdkVersion` — minimum supported vs. highest optimized
- `targetSdkVersion` does NOT block the app from running on newer Android versions
- build.gradle (Module: app) is **different** from build.gradle (Project)
- Package name should **not** be changed after publishing to Google Play
- The Build Number tap count is **7** to enable Developer Options
- Log tag should be a **constant** (`private static final String`)
- `Log.d` = Debug, not Default

---

## Quick Revision Bullets
- Android Studio = official Java IDE for Android; uses Gradle build system
- Manifest must declare every activity; main activity needs MAIN action + LAUNCHER category
- `minSdkVersion` sets the minimum Android version; `targetSdkVersion` sets the highest optimized
- AVD Manager creates virtual devices for testing; always start emulator once per session
- Enable USB Debugging by tapping Build Number 7 times in device Settings
- `Log.d(TAG, "msg")` — debug; `Log.e` = error; use `getSimpleName()` for log tag
- After changing build.gradle, always click "Sync Now"

---
---

# CHAPTER 1.2: Layouts, Views and Resources

## Concept Overview
**Views** are the UI building blocks of Android. Everything you see on screen is a View. Views are organized into a **hierarchy** (ViewGroup contains Views and other ViewGroups). Layouts are specialized ViewGroups that position their children.

**MVP Pattern:**
- **Views** — UI elements that display data and respond to user actions
- **Presenters** — connect views to model; supply data and handle user input
- **Model** — specifies data structure and logic

---

## Theory & Logic

### The View Hierarchy

```
ViewGroup (root layout)
├── View (Button)
├── ViewGroup (LinearLayout)
│   ├── View (TextView)
│   └── View (Button)
└── View (ImageView)
```

- **View** = basic building block for all UI components
- Has: location (left, top coordinates), dimensions (width, height) in **dp** (device-independent pixels)
- Hundreds of predefined views: TextView, EditText, Button, ScrollView, RecyclerView, ImageView, etc.

### ViewGroups (Layout Types)

| Layout | Description |
|--------|-------------|
| **LinearLayout** | Children positioned/aligned horizontally OR vertically |
| **RelativeLayout** | Children positioned relative to each other or parent |
| **ConstraintLayout** | Positions via anchor points, edges, guidelines; easy drag-and-drop in editor |
| **TableLayout** | Children arranged in rows and columns |
| **AbsoluteLayout** | Exact x/y coordinates — avoid; inflexible |
| **FrameLayout** | Stack of children; most recently added child is on top |
| **GridLayout** | Rectangular grid; can scroll |
| **ScrollView** | Contains ONE child; enables vertical scrolling |
| **RecyclerView** | Scrollable list; adds/removes views dynamically for efficiency |

### XML Layout Basics

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <Button
        android:id="@+id/button_toast"
        android:layout_width="@dimen/my_view_width"
        android:layout_height="wrap_content"
        android:text="@string/button_label_toast"
        android:onClick="showToast" />

    <TextView
        android:id="@+id/show_count"
        android:layout_width="@dimen/my_view_width"
        android:layout_height="@dimen/counter_height"
        android:background="@color/myBackgroundColor"
        android:textStyle="bold"
        android:text="@string/count_initial_value" />

</LinearLayout>
```

### XML Attributes Deep Dive

**Identifying/Referencing Views:**
```xml
android:id="@+id/button_count"    <!-- @+id = CREATE new id -->
android:layout_toLeftOf="@id/show_count"  <!-- @id = REFERENCE existing id -->
```

**Layout Width/Height values:**
- `match_parent` — expands to fill parent
- `wrap_content` — shrinks to fit content
- Fixed dp value (e.g., `16dp`) — device-independent pixels

**LinearLayout-specific:**
```xml
android:orientation="horizontal"   <!-- or "vertical" -->
android:layout_gravity="center_horizontal"  <!-- position within parent -->
android:padding="8dp"              <!-- space between view edge and content -->
android:paddingTop="4dp"
android:paddingBottom="4dp"
android:paddingLeft="8dp"
android:paddingRight="8dp"
android:paddingStart="8dp"         <!-- use instead of paddingLeft for RTL support -->
android:paddingEnd="8dp"
```

**RelativeLayout positioning:**
```xml
android:layout_toLeftOf="@id/other_view"
android:layout_toRightOf="@id/other_view"
android:layout_centerHorizontal="true"
android:layout_centerVertical="true"
android:layout_alignParentTop="true"
android:layout_alignParentBottom="true"
```

**Style attributes:**
```xml
android:background="@color/myBackgroundColor"   <!-- color or drawable -->
android:text="@string/hello"                    <!-- text content -->
android:textColor="@color/colorPrimary"
android:textSize="20sp"                         <!-- use sp for text -->
android:textStyle="bold"                        <!-- normal, bold, italic, bold|italic -->
```

### Resource Files

**Syntax for referencing resources in XML:**
```
@package_name:resource_type/resource_name
```
- `package_name` = omitted when referencing own project resources
- `resource_type` = string, color, dimen, drawable, etc.
- `resource_name` = the name attribute value

**Examples:**
```xml
android:text="@string/button_label_toast"           <!-- own project resource -->
android:background="@color/colorPrimary"             <!-- own project resource -->
android:textColor="@android:color/white"             <!-- Android system resource -->
```

### strings.xml

```xml
<resources>
    <string name="app_name">Hello Toast</string>
    <string name="button_label_count">Count</string>
    <string name="button_label_toast">Toast</string>
    <string name="count_initial_value">0</string>
</resources>
```

**To extract hard-coded strings in Android Studio:** Click string → Alt+Enter (Windows) / Option+Return (Mac) → Extract string resource

### colors.xml

```xml
<resources>
    <color name="colorPrimary">#3F51B5</color>    <!-- hex: #RGB, #RRGGBB, #ARGB, #AARRGGBB -->
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
    <color name="myBackgroundColor">#FFF043</color>
</resources>
```

### dimens.xml

```xml
<resources>
    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>
    <dimen name="my_view_width">300dp</dimen>
    <dimen name="count_text_size">200sp</dimen>  <!-- sp for text sizes -->
    <dimen name="counter_height">300dp</dimen>
</resources>
```

**dp vs sp:**
- `dp` (device-independent pixels) — for layouts, margins, padding; doesn't scale with font size
- `sp` (scaleable pixels) — for text; also scales with user's font size preference

### Standard Resource Folders

| Folder | Contents |
|--------|----------|
| `drawable/` | Images and icons (WebP, PNG, 9-patch, JPG, GIF) |
| `layout/` | XML layout files |
| `menu/` | XML menu resource files |
| `mipmap/` | Optimized launcher icons for different densities |
| `values/` | strings.xml, colors.xml, dimens.xml, styles.xml |

---

## Code: Responding to View Clicks

### Method 1: android:onClick attribute (simplest)

```xml
<!-- XML layout -->
<Button
    android:id="@+id/button_toast"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_label_toast"
    android:onClick="showToast" />   <!-- calls showToast() in the activity -->
```

```java
// Activity Java code
// Method MUST be: public, return void, take a View parameter
public void showToast(View view) {
    // Do something in response to button click
    Toast.makeText(this, "Hello!", Toast.LENGTH_SHORT).show();
}
```

### Method 2: Updating Views Programmatically

```java
// Step 1: Get the view object using its resource ID
// (TextView) cast is needed because findViewById returns View
TextView mShowCount = (TextView) findViewById(R.id.show_count);

// Step 2: Update the view — this updates what's displayed on screen
mShowCount.setText(Integer.toString(mCount));
```

**Full example — CountUp method:**
```java
private int mCount = 0;
private TextView mShowCount;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // Get the TextView reference once, store in member variable
    mShowCount = (TextView) findViewById(R.id.show_count);
}

// Called when the Count button is clicked (via android:onClick)
public void countUp(View view) {
    mCount++;                                    // increment count
    if (mShowCount != null) {
        mShowCount.setText(Integer.toString(mCount));  // update the display
    }
}
```

**Trace/Dry-run:** Suppose mCount = 3. User taps Count.
- `mCount++` → mCount = 4
- `Integer.toString(4)` → "4"
- `mShowCount.setText("4")` → TextView now shows "4"

---

## Common Exam Traps / Edge Cases
- `@+id` **creates** a new id; `@id` **references** an existing id — never confuse the two
- `match_parent` fills parent; `wrap_content` shrinks to content; they are NOT the same as `fill_parent` (deprecated) though functionally `fill_parent` = `match_parent`
- `dp` for layouts, `sp` for text sizes — don't mix them up
- `ScrollView` can only have **one** direct child view
- `FrameLayout` draws children in a **stack** (last = on top)
- `android:padding` is different from `android:layout_margin`:
  - Padding = space between view's edge and its own content
  - Margin = space between view's edge and its parent's edge (set via `android:layout_margin`)
- Resource reference format: `@package:type/name` (omit package if it's your own project)
- `android:textSize` uses `sp` not `dp` for accessibility (respects user's font size setting)

---

## Quick Revision Bullets
- View = basic UI building block; ViewGroup contains views; Layout = specialized ViewGroup
- `match_parent`, `wrap_content`, or fixed dp for width/height
- Resource syntax: `@[package:]type/name`; own project resources omit package name
- android:id with `@+id/name` creates; `@id/name` references
- `sp` for text sizes (scales with font preference); `dp` for everything else
- `onClick` attribute must point to a method that is `public void methodName(View view)`
- `findViewById(R.id.view_id)` returns a View; must cast to specific type (e.g., TextView)
- strings.xml, colors.xml, dimens.xml live in `res/values/`

---
---

# CHAPTER 1.3: Text and Scrolling Views

## Concept Overview
**TextView** is one of the most frequently used views — it displays text on screen. **ScrollView** enables scrolling when content exceeds screen height. Key distinction: ScrollView can only have one direct child.

---

## Theory & Logic

### TextView

```xml
<TextView
    android:id="@+id/show_count"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/myBackgroundColor"
    android:text="@string/hello_world"
    android:textColor="@color/colorPrimary"
    android:textAppearance="@android:style/TextAppearance"
    android:textSize="20sp"
    android:textStyle="bold"           <!-- normal, bold, italic, bold|italic -->
    android:typeface="monospace"       <!-- normal, sans, serif, monospace -->
    android:lineSpacingExtra="4sp"
    android:autoLink="web"             <!-- none, web, email, phone, map, all -->
/>
```

**Important TextView attributes:**
- `android:text` — the displayed string
- `android:textColor` — color value, resource, or theme
- `android:textAppearance` — predefined style resource (sets color, typeface, style, size)
- `android:textSize` — use `sp` (e.g., `20sp`, `14.5sp`)
- `android:textStyle` — `normal`, `bold`, `italic`, `bold|italic`
- `android:typeface` — `normal`, `sans`, `serif`, `monospace`
- `android:lineSpacingExtra` — extra spacing between lines
- `android:autoLink` — auto-converts URLs/emails/phones/addresses to clickable links

**Supported HTML tags in text:**
- `<b>bold text</b>`
- `<i>italic text</i>`
- `<b><i>bold italic</i></b>`

**Long strings in strings.xml:**
```xml
<string name="article_text">
First paragraph text here.\n
\n
Second paragraph with a blank line before it.\n
</string>
```
- `\n` = end of line
- Two `\n\n` = blank line (new paragraph)
- Apostrophes must be escaped: `\'`
- Double quotes must be escaped: `\"`

### Referring to a TextView in Java

```java
// Step 1: Get the view by its resource ID
TextView mShowCount = (TextView) findViewById(R.id.show_count);

// Step 2: Update the text
mShowCount.setText(mCount_text);  // sets new text content
```

### ScrollView

```xml
<ScrollView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/article_heading">

    <!-- ScrollView can only have ONE direct child -->
    <LinearLayout
        android:layout_width="match_parent"     <!-- match ScrollView width -->
        android:layout_height="wrap_content"    <!-- wrap content height -->
        android:orientation="vertical">         <!-- must be vertical for ScrollView -->

        <TextView
            android:id="@+id/article_subheading"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="@dimen/padding_regular"
            android:text="@string/article_subtitle"
            android:textAppearance="@android:style/TextAppearance" />

        <TextView
            android:id="@+id/article"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:autoLink="web"
            android:lineSpacingExtra="@dimen/line_spacing"
            android:text="@string/article_text" />

    </LinearLayout>
</ScrollView>
```

**Rules for ScrollView:**
- `ScrollView` = vertical scrolling; `HorizontalScrollView` = horizontal scrolling
- `ScrollView` is a subclass of `FrameLayout` — can only have **one** direct child
- That child is usually a `LinearLayout` with `android:orientation="vertical"`
- Child `LinearLayout` should use `android:layout_width="match_parent"` and `android:layout_height="wrap_content"`

### ScrollView Performance Considerations
- **All views are in memory** even if not on screen — great for free-form text but memory-intensive
- For long lists with images → use **RecyclerView** instead (adds/removes views dynamically)
- Deeply nested `LinearLayout` with `layout_weight` → very expensive (measured twice)
- For complex layouts → use **RelativeLayout** or **GridLayout** for flatter hierarchy
- Images in ScrollView → can cause performance issues; use **AsyncTask** to load in background

---

## Code: Complete ScrollView Example

```xml
<!-- res/layout/activity_main.xml -->
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Fixed heading - NOT inside ScrollView -->
    <TextView
        android:id="@+id/article_heading"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/article_title"
        android:textStyle="bold"
        android:textSize="24sp" />

    <!-- ScrollView positioned BELOW the heading -->
    <ScrollView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/article_heading">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <TextView
                android:id="@+id/article_subheading"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="@string/article_subtitle" />

            <TextView
                android:id="@+id/article"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:autoLink="web"
                android:lineSpacingExtra="@dimen/line_spacing"
                android:text="@string/article_text" />

        </LinearLayout>
    </ScrollView>
</RelativeLayout>
```

**What this does:** The heading is fixed at the top; only the subheading + article text scrolls.

---

## Common Exam Traps / Edge Cases
- ScrollView can have **only one** direct child (not multiple children directly)
- `HorizontalScrollView` for horizontal scrolling, `ScrollView` for vertical — don't mix up
- `ScrollView` extends `FrameLayout` — this is why only one child is allowed
- Nested `LinearLayout` with `layout_weight` is expensive — each child measured **twice**
- All ScrollView content is in memory simultaneously — bad for long lists; use RecyclerView instead
- `android:autoLink="web"` only works on `TextView`, not on other view types

---

## Quick Revision Bullets
- TextView displays text; EditText is its editable subclass
- `sp` for textSize (scales with accessibility font preference)
- HTML tags supported in TextView: `<b>`, `<i>`, and their combination
- ScrollView = vertical; HorizontalScrollView = horizontal; both extend FrameLayout
- ScrollView can contain **only one** direct child (usually a LinearLayout)
- LinearLayout inside ScrollView: `layout_width="match_parent"`, `layout_height="wrap_content"`, `orientation="vertical"`
- For long lists → use RecyclerView (more efficient); ScrollView loads everything into memory

---
---

# CHAPTER 2.1: Understanding Activities and Intents

## Concept Overview
An **Activity** represents a single screen in your app with an interface the user can interact with. **Intents** are message objects that request the Android runtime to start an Activity or other component. The system manages a **back stack** of activities.

**Mental model:** Activities are like web pages; the back stack is like the browser history. Intents are like HTTP requests — they carry the destination and data.

---

## Theory & Logic

### About Activities
- Each activity = one screen with a user interface
- Activities are **independent** of each other
- One activity is the **"main"** activity (shown when app launches)
- Each time a new activity starts → previous activity is **stopped** (not destroyed) and pushed to back stack
- Back button → pops top activity, destroys it, resumes the previous one

### Creating an Activity — Three Required Steps
1. **Create an Activity Java class** (extends AppCompatActivity)
2. **Implement a user interface** (XML layout)
3. **Declare the activity in AndroidManifest.xml**

### Activity Java Class

```java
// All activities extend AppCompatActivity (or Activity)
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);      // always call super
        setContentView(R.layout.activity_main); // inflate layout (REQUIRED)
    }
}
```

### Declaring Activity in AndroidManifest.xml

```xml
<application ... >
    <!-- Main (parent) activity -->
    <activity android:name=".MainActivity">
        <intent-filter>
            <!-- MAIN = entry point; LAUNCHER = show in app launcher -->
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>

    <!-- Child activity (no intent filter needed for internal use only) -->
    <activity
        android:name=".SecondActivity"
        android:label="@string/activity2_name"
        android:parentActivityName=".MainActivity">
        <!-- For backward compat (pre-API 16) -->
        <meta-data
            android:name="android.support.PARENT_ACTIVITY"
            android:value="com.example.android.twoactivities.MainActivity" />
    </activity>
</application>
```

**Rules:**
- **Only the main activity** should have the MAIN action + LAUNCHER category intent filter
- Every activity MUST be declared in the manifest
- `android:parentActivityName` declares the activity's parent (for Up navigation)

### About Intents

**Definition:** An **Intent** is a message object that makes a request to the Android runtime to start an activity or other component.

**Two types:**
1. **Explicit Intent** — specifies the receiving activity's exact class name. Use for activities within your own app.
2. **Implicit Intent** — specifies only a general action; Android matches to available activities. Use for actions that other apps can handle (e.g., share text, open URL).

**Key Intent Fields:**
- **Activity class** (for explicit): the class name of the target component
- **Intent data**: a URI representing the data to act on
- **Intent extras**: key-value pairs with additional information
- **Intent flags**: metadata bits controlling how activity is launched

### Starting an Activity with an Explicit Intent

```java
// Create explicit intent specifying the class to launch
Intent messageIntent = new Intent(this, ShowMessageActivity.class);
//                              context  target activity class

// Start the activity — system pushes current activity to back stack
startActivity(messageIntent);
```

**Closing an Activity:**
```java
// Close the current activity and return to the one that started it
public void closeActivity(View view) {
    finish();
}
```

### Passing Data Between Activities

**In the sending activity:**

```java
// Define key constants with fully-qualified names to avoid conflicts
public final static String EXTRA_MESSAGE = "com.example.mysampleapp.MESSAGE";
public final static String EXTRA_POSITION_X = "com.example.mysampleapp.X";
public final static String EXTRA_POSITION_Y = "com.example.mysampleapp.Y";

// Create intent
Intent messageIntent = new Intent(this, ShowMessageActivity.class);

// Method 1: Add extras directly
messageIntent.putExtra(EXTRA_MESSAGE, "this is my message");  // String
messageIntent.putExtra(EXTRA_POSITION_X, 100);                // int
messageIntent.putExtra(EXTRA_POSITION_Y, 500);                // int

// Method 2: Bundle extras together
Bundle extras = new Bundle();
extras.putString(EXTRA_MESSAGE, "this is my message");
extras.putInt(EXTRA_POSITION_X, 100);
extras.putInt(EXTRA_POSITION_Y, 500);
messageIntent.putExtras(extras);   // note: putExtras (plural)

// Add URI data (only one URI allowed; last call wins)
messageIntent.setData(Uri.parse("http://www.google.com"));
messageIntent.setData(Uri.fromFile(new File("/sdcard/sample.jpg")));
messageIntent.setData(Uri.parse("content://mysample.provider/data"));

startActivity(messageIntent);
```

**In the receiving activity:**

```java
// Get the intent that started this activity
Intent intent = getIntent();

// Get URI data
Uri locationUri = intent.getData();

// Get extras (use the SAME key constants defined in the sending activity)
String message = intent.getStringExtra(MainActivity.EXTRA_MESSAGE);
int positionX = intent.getIntExtra(MainActivity.EXTRA_POSITION_X, 0); // 0 = default
int positionY = intent.getIntExtra(MainActivity.EXTRA_POSITION_Y, 0);

// OR get the entire bundle and extract
Bundle extras = intent.getExtras();
String message = extras.getString(MainActivity.EXTRA_MESSAGE);
```

**Intent Data vs Intent Extras:**
- **Data**: single URI; use when you have one piece of location-based info
- **Extras**: key-value pairs; use for multiple pieces of info or non-URI data

### Getting Data Back from an Activity

**In the sending (originating) activity:**

```java
// Define request codes as constants (must be unique)
public static final int TEXT_REQUEST = 1;
public static final int PHOTO_REQUEST = 2;

// Start activity expecting a result back
startActivityForResult(messageIntent, TEXT_REQUEST);

// Handle the returned data
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    if (requestCode == TEXT_REQUEST) {       // which request?
        if (resultCode == RESULT_OK) {       // successful?
            String reply = data.getStringExtra(SecondActivity.EXTRA_RETURN_MESSAGE);
            // process the returned data
        }
    }
}
```

**In the launched (responding) activity:**

```java
public final static String EXTRA_RETURN_MESSAGE = "com.example.mysampleapp.RETURN_MESSAGE";

// When done, send data back
Intent returnIntent = new Intent();   // new empty intent (not the original)
returnIntent.putExtra(EXTRA_RETURN_MESSAGE, mMessage);

// Set result and close
setResult(RESULT_OK, returnIntent);  // RESULT_OK, RESULT_CANCELED, RESULT_FIRST_USER
finish();  // close this activity and return to calling activity
```

**Result codes:**
- `RESULT_OK` — request successful
- `RESULT_CANCELED` — user cancelled operation
- `RESULT_FIRST_USER` — starting point for custom result codes

### Activity Navigation

**Back Navigation (Temporal):**
- Device Back button
- Last-in, first-out (LIFO) back stack
- Activities pushed when started, popped when Back pressed or `finish()` called
- Managed automatically by the system

```
Back Stack:
[MainActivity] [EmailList] [SingleEmail]  ← current
                                 ↑
                              Back button pops this, resumes EmailList
```

**Up Navigation (Ancestral):**
- The ← arrow in the action bar (app bar)
- Navigates UP the app's hierarchy
- Defined by `android:parentActivityName` in manifest
- Up ≠ Back necessarily (Up is based on logical hierarchy, not history)

**Implementing Up navigation:**
```xml
<!-- In the manifest -->
<activity
    android:name=".SecondActivity"
    android:parentActivityName=".MainActivity">
    <meta-data
        android:name="android.support.PARENT_ACTIVITY"
        android:value="com.example.MainActivity" />
</activity>
```

---

## Code: Complete Two-Activity Example

### MainActivity.java (Sending)

```java
public class MainActivity extends AppCompatActivity {

    // Define extra keys as public constants
    public final static String EXTRA_MESSAGE = "com.example.mysampleapp.MESSAGE";
    public static final int TEXT_REQUEST = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    // Called when Send button is clicked
    public void launchSecondActivity(View view) {
        // Get text from EditText
        EditText editText = (EditText) findViewById(R.id.editText_main);
        String message = editText.getText().toString();

        // Build the intent with the message as an extra
        Intent intent = new Intent(this, SecondActivity.class);
        intent.putExtra(EXTRA_MESSAGE, message);

        // Start with result if we need data back
        startActivityForResult(intent, TEXT_REQUEST);
    }

    @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (requestCode == TEXT_REQUEST) {
            if (resultCode == RESULT_OK) {
                // Get the returned message
                String reply = data.getStringExtra(SecondActivity.EXTRA_REPLY);
                TextView textView = (TextView) findViewById(R.id.text_reply);
                textView.setText(reply);
            }
        }
    }
}
```

### SecondActivity.java (Receiving + Returning)

```java
public class SecondActivity extends AppCompatActivity {

    public static final String EXTRA_REPLY = "com.example.mysampleapp.REPLY";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);

        // Get the intent that started this activity
        Intent intent = getIntent();

        // Extract the message
        String message = intent.getStringExtra(MainActivity.EXTRA_MESSAGE);

        // Display the message
        TextView textView = (TextView) findViewById(R.id.text_message);
        textView.setText(message);
    }

    // Called when Reply button is clicked
    public void returnReply(View view) {
        // Get the reply text
        EditText editText = (EditText) findViewById(R.id.editText_second);
        String reply = editText.getText().toString();

        // Build return intent
        Intent replyIntent = new Intent();          // new empty intent
        replyIntent.putExtra(EXTRA_REPLY, reply);

        // Set result and close
        setResult(RESULT_OK, replyIntent);
        finish();
    }
}
```

---

## Common Exam Traps / Edge Cases
- `startActivity()` vs `startActivityForResult()` — the second expects data to come back
- `setResult()` must be called BEFORE `finish()` in the launched activity
- The return intent in the launched activity should be a **new** Intent (not reuse the original)
- `onActivityResult()` has THREE parameters: `requestCode`, `resultCode`, `data` (the returned intent)
- `android:parentActivityName` for Up navigation — only works API 16+; use `<meta-data>` for older
- EXTRA keys should be defined as constants with fully-qualified names to avoid collisions
- Only the **main activity** should have MAIN + LAUNCHER intent filters
- `finish()` closes the current activity and removes it from the back stack
- Intent data = single URI; can only call `setData()` once (last call wins)

---

## Quick Revision Bullets
- Activity = one screen; every activity must be declared in AndroidManifest.xml
- Intent types: Explicit (specific class) and Implicit (general action)
- Main activity needs MAIN action + LAUNCHER category in manifest
- `startActivity(intent)` starts; `startActivityForResult(intent, requestCode)` to get data back
- Pass data via intent extras (`putExtra`/`getStringExtra`) or intent data (URI)
- Returned data: `setResult(RESULT_OK, replyIntent)` → `finish()` → received in `onActivityResult()`
- Back stack = LIFO; Back button pops and destroys top activity; Up = logical parent hierarchy
- Define extra keys as `public static final String` constants with package-prefixed names

---
---

# CHAPTER 2.2: The Activity Lifecycle and Managing State

## Concept Overview
Every Activity goes through a series of states from creation to destruction — this is the **Activity Lifecycle**. The Android system calls **callback methods** at each lifecycle transition. Understanding the lifecycle is critical for managing resources properly.

**Mental model:** Think of an activity like a stage performer. They're *Created*, then *Started* (visible), then *Resumed* (performing), then *Paused* (lights dimmed), then *Stopped* (off stage), then *Destroyed* (done for the night). The performer must prepare and clean up at each transition.

---

## Theory & Logic

### Lifecycle States & Callbacks

```
                    ┌─────────────────────────────────┐
                    │         Activity Created          │
                    │           onCreate()              │
                    └─────────────────────────────────┘
                                    │
                                    ▼
                    ┌─────────────────────────────────┐
                    │         Activity Started         │
                    │           onStart()               │
                    └─────────────────────────────────┘
                                    │
                                    ▼
                    ┌─────────────────────────────────┐
◄───onRestart()───  │        Activity Resumed          │  ←─────────
(from stopped)      │           onResume()              │           │
                    └─────────────────────────────────┘           │
                                    │                              │
                                    ▼                              │
                    ┌─────────────────────────────────┐           │
                    │         Activity Paused          │           │
                    │           onPause()               │           │
                    └─────────────────────────────────┘           │
                                    │                              │
                      ┌─────────────┴─────────────┐              │
                      ▼                           ▼               │
          ┌─────────────────────┐    ┌────────────────────────┐  │
          │  Activity Stopped   │    │    Activity Destroyed   │  │
          │     onStop()        │    │     onDestroy()          │  │
          └─────────────────────┘    └────────────────────────┘  │
                      │                                            │
                      └──────────────── onRestart() ──────────────┘
```

### Each Callback in Detail

#### onCreate() — REQUIRED
```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);  // always call super first
    // Initialize activity:
    setContentView(R.layout.activity_main);  // inflate layout
    // Get views, set up listeners, initialize variables
    mShowCount = (TextView) findViewById(R.id.show_count);
}
```
- Called **once** when activity is first created
- Only required callback
- Initialize UI, assign variables, set up background tasks
- Created state is **transient** — immediately moves to started

#### onStart() — Activity Becomes Visible
```java
@Override
protected void onStart() {
    super.onStart();
    // Activity about to become visible
    // Re-register resources released in onStop()
    // (e.g., re-register GPS listeners)
}
```
- Called after `onCreate()` and when returning from stopped state
- May be called **multiple times** during lifecycle
- User cannot interact yet (that starts in `onResume()`)
- Pair with `onStop()`

#### onResume() — Activity Running (Foreground)
```java
@Override
protected void onResume() {
    super.onResume();
    // Activity is visible and user is interacting
    // Restart any paused animations or video
    // Re-register sensors if released in onPause()
}
```
- Activity is in **foreground**, user can interact
- May be called multiple times (every time app comes back from paused)
- Pair with `onPause()`
- Called just after `onStart()` initially

#### onPause() — First Signal User is Leaving
```java
@Override
protected void onPause() {
    super.onPause();
    // First indication user may be leaving
    // Stop animations, video playback
    // Release CPU-intensive resources
    // Commit unsaved changes (e.g., draft email)
    // DO NOT perform heavy operations here
}
```
- Called when: activity going into background, dialog overlaid, split-screen mode where other app has focus
- Must execute **QUICKLY** — don't do heavy work (e.g., writing to database)
- From paused: can resume (user returns) or stop (user leaves)
- Note: In multi-window mode (API 24), paused activity may still be fully visible

#### onStop() — Activity No Longer Visible
```java
@Override
protected void onStop() {
    super.onStop();
    // Activity not visible (user started another activity or went to Home)
    // Release remaining resources
    // Perform heavy operations (e.g., save to database)
    // Unregister GPS, sensors
}
```
- Called when activity is no longer visible
- System retains activity in back stack; may restart later
- Stopped activities may be **killed by system** if resources are low
- Pair with `onStart()`

#### onDestroy()
```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // Activity about to be destroyed
    // Final cleanup — release all remaining resources
    // Stop background threads
}
```
- Called when: `finish()` called, user navigates back, low memory, **configuration change**
- **Do NOT rely** on `onDestroy()` for saving critical data — use `onPause()` or `onStop()` instead
- System may kill the process without calling `onDestroy()`

#### onRestart()
```java
@Override
protected void onRestart() {
    super.onRestart();
    // Transient state — called when stopped activity is restarted
}
```
- Only called if a stopped activity is started again (not when first creating)
- Called between `onStop()` and `onStart()`
- Usually implement behavior in `onStop()`/`onStart()` instead of here

### Configuration Changes
When device configuration changes (rotation, locale change, multi-window mode), Android:
1. **Destroys** the activity: `onPause()` → `onStop()` → `onDestroy()`
2. **Recreates** it: `onCreate()` → `onStart()` → `onResume()`

This means all activity state (member variables, scroll position, etc.) is **lost** unless you save it.

### Instance State — Saving and Restoring

**What is automatically saved?**
- State of Views with unique `android:id` attributes (e.g., text typed in EditText)
- The Intent that started the activity

**What is NOT automatically saved?**
- Your own member variables
- Most other runtime data

**Saving state with onSaveInstanceState():**
```java
@Override
public void onSaveInstanceState(Bundle savedInstanceState) {
    super.onSaveInstanceState(savedInstanceState);  // MUST call super (saves view state)

    // Save your own state data
    savedInstanceState.putInt("score", mCurrentScore);
    savedInstanceState.putInt("level", mCurrentLevel);
    savedInstanceState.putString("username", mUsername);
    // Bundle methods: putInt, putString, putBoolean, putFloat, putDouble, putStringArray, etc.
}
```

**Restoring state in onCreate():**
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    if (savedInstanceState != null) {
        // Activity is being recreated — restore saved state
        mCurrentScore = savedInstanceState.getInt("score");
        mCurrentLevel = savedInstanceState.getInt("level");
        mUsername = savedInstanceState.getString("username");
    } else {
        // Activity created fresh — initialize with default values
        mCurrentScore = 0;
        mCurrentLevel = 1;
    }
}
```

**Alternative: Restore in onRestoreInstanceState():**
```java
@Override
protected void onRestoreInstanceState(Bundle savedInstanceState) {
    super.onRestoreInstanceState(savedInstanceState);
    // Called after onStart(); bundle guaranteed non-null here
    mCurrentScore = savedInstanceState.getInt("score");
}
```

**When is instance state saved?**
- Before the activity is stopped (just before `onStop()`)
- Only across **configuration changes** or **system killing stopped activities**
- NOT preserved when user force-quits, reboots device, or app process is killed
- For persistent storage → use **SharedPreferences** or database

---

## Lifecycle Dry-Run: Device Rotation

Initial state: MainActivity running
1. User rotates device
2. System calls: `onPause()` → `onStop()` → `onSaveInstanceState()` → `onDestroy()`
3. System calls: `onCreate(bundle)` → `onStart()` → `onResume()`
4. In `onCreate()`, `bundle != null`, so restore saved state

---

## Common Exam Traps / Edge Cases
- `onCreate()` is called **once** (on creation); `onResume()` can be called many times
- `onPause()` must be **FAST** — don't do heavy DB writes here; do that in `onStop()`
- `onDestroy()` is NOT guaranteed to be called — don't rely on it for critical saves
- Instance state survives **configuration changes** and system killing, but NOT force-quit or reboot
- `super.onSaveInstanceState()` must be called to save view hierarchy state
- `savedInstanceState` in `onCreate()` can be **null** (first launch) — always check before using
- **Configuration changes** include: rotation, locale change, multi-window mode
- `onRestart()` is only called for stopped→started transitions; not on fresh launch

---

## Quick Revision Bullets
- 7 lifecycle states: Created, Started, Resumed, Paused, Stopped, Destroyed, Restarted
- Only required callback: `onCreate()` (must call `setContentView()` here)
- `onPause()` = first signal user leaving; must be fast; paired with `onResume()`
- `onStop()` = activity invisible; do heavy operations here; paired with `onStart()`
- `onDestroy()` = NOT guaranteed; don't rely on it for saving data
- Configuration changes (rotation) → destroy + recreate activity
- Save state in `onSaveInstanceState(bundle)`, restore in `onCreate(bundle)` (check for null!)
- Instance state: persists across rotation/system kill; NOT across force-quit/reboot

---
---

# CHAPTER 2.3: Activities and Implicit Intents

## Concept Overview
**Implicit Intents** specify a general action to perform without naming a specific component. The Android system matches the intent with available activities via **Intent Filters** declared in the manifest.

---

## Theory & Logic

### Implicit Intent Components
An implicit intent can specify:
1. **Action** — the generic action (e.g., `ACTION_VIEW`, `ACTION_SEND`); defined as constants in `Intent` class starting with `ACTION_`
2. **Category** — additional info about the handler (optional); constants start with `CATEGORY_`
3. **Data type** — MIME type of data the activity should operate on

### Sending Implicit Intents

```java
// Step 1: Create implicit intent with an action
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);

// OR: create with action directly
Intent sendIntent = new Intent(Intent.ACTION_SEND);

// Step 2: Add data (MIME type and/or URI)
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType("text/plain");

// Step 3: ALWAYS resolve before starting (to prevent crash)
if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(sendIntent);
}
```

**WARNING:** If `resolveActivity()` returns `null`, there is no app to handle the intent. Calling `startActivity()` will **crash** your app. Always check first!

### Showing the App Chooser

```java
Intent sendIntent = new Intent(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType("text/plain");

// Always show chooser (even if user has a default app)
String title = getResources().getString(R.string.chooser_title);
Intent chooser = Intent.createChooser(sendIntent, title);

if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(chooser);
}
```

Use the chooser when you want the user to pick an app each time (e.g., share functions).

### Setting Data on Intent

```java
// Web URL
messageIntent.setData(Uri.parse("http://www.google.com"));

// File URI
messageIntent.setData(Uri.fromFile(new File("/sdcard/sample.jpg")));

// Content URI
messageIntent.setData(Uri.parse("content://mysample.provider/data"));

// Custom URI
messageIntent.setData(Uri.parse("custom:" + dataID + buttonId));
```

### Receiving Implicit Intents — Intent Filters

```xml
<activity android:name="ShareActivity">
    <intent-filter>
        <!-- Action the activity can handle -->
        <action android:name="android.intent.action.SEND"/>

        <!-- DEFAULT category is REQUIRED for all implicit intents -->
        <category android:name="android.intent.category.DEFAULT"/>

        <!-- MIME type of data accepted -->
        <data android:mimeType="text/plain"/>
    </intent-filter>
</activity>
```

**Intent Filter elements:**
- `<action>` — the intent action (at least one required)
- `<category>` — intent category; `android.intent.category.DEFAULT` is required for implicit intents
- `<data>` — URI scheme, host, port, path, and/or MIME type

**Matching rules:**
- Intent must pass ALL three tests (action, category, data) for the filter to match
- Multiple `<action>` elements in one filter = OR logic
- One activity can have multiple `<intent-filter>` elements

**Example with multiple actions:**
```xml
<intent-filter>
    <action android:name="android.intent.action.EDIT" />
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```

**Example with data constraints:**
```xml
<intent-filter>
    <data android:mimeType="video/mpeg" android:scheme="http" />
    <data android:mimeType="audio/mpeg" android:scheme="http" />
</intent-filter>
```

**Handling the received intent:**
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_share);

    Intent intent = getIntent();           // get the intent
    Uri locationUri = intent.getData();    // get URI data
    String text = intent.getStringExtra(Intent.EXTRA_TEXT);  // get extra

    // Use the data...
}
```

### ShareCompat.IntentBuilder (Easier Sharing)

```java
// Chain methods for easy sharing
ShareCompat.IntentBuilder
    .from(this)                               // context of calling activity
    .setType(mimeType)                         // MIME type of data
    .setChooserTitle("Share this text with: ") // chooser dialog title
    .setText(txt)                              // the text to share
    .startChooser();                           // sends the intent
```

### Managing Tasks and the Back Stack

**Activity Launch Modes** (defined in manifest or via intent flags):

| Launch Mode | Behavior |
|-------------|----------|
| `standard` (default) | New activity always created; multiple instances possible in same task |
| `singleTop` | If activity is at TOP of back stack, routes to existing instance (calls `onNewIntent()`); otherwise creates new |
| `singleTask` | Creates new task; if instance exists in any task, routes to it |
| `singleInstance` | Single activity, always alone in its task |

```xml
<activity
    android:name=".SecondActivity"
    android:launchMode="singleTop">
</activity>
```

**Intent Flags** (override launchMode):
- `FLAG_ACTIVITY_NEW_TASK` — start in new task (same as singleTask)
- `FLAG_ACTIVITY_SINGLE_TOP` — if at top, route to existing (same as singleTop)
- `FLAG_ACTIVITY_CLEAR_TOP` — if instance exists in back stack, destroy activities above it and route to it

```java
Intent intent = new Intent(this, SecondActivity.class);
intent.addFlag(Intent.FLAG_ACTIVITY_CLEAR_TOP);
startActivity(intent);
```

**Handling new intents in singleTop/singleTask:**
```java
@Override
public void onNewIntent(Intent intent) {
    super.onNewIntent(intent);
    setIntent(intent);  // update the stored intent so getIntent() returns new one
}
```

**Task Affinities:**
```xml
<activity
    android:name=".SecondActivity"
    android:taskAffinity="com.example.android.myapp.newtask"
    android:allowTaskReparenting="true">
</activity>
```
- Default affinity = package name
- Used with `singleTask` or `FLAG_ACTIVITY_NEW_TASK` to place activity in named task
- `allowTaskReparenting` enables reparenting from launching task to affinity task

---

## Code: Complete Implicit Intent Example (Sharing Text)

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    // Called when Share button is clicked
    public void shareText(View view) {
        EditText editText = (EditText) findViewById(R.id.editText);
        String textMessage = editText.getText().toString();

        // Build implicit intent
        Intent sendIntent = new Intent();
        sendIntent.setAction(Intent.ACTION_SEND);
        sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
        sendIntent.setType("text/plain");

        // Always use chooser for sharing
        String title = getString(R.string.chooser_title);
        Intent chooser = Intent.createChooser(sendIntent, title);

        // Resolve before starting — prevents crash if no app available
        if (sendIntent.resolveActivity(getPackageManager()) != null) {
            startActivity(chooser);
        }
    }
}
```

---

## Common Exam Traps / Edge Cases
- **Always call `resolveActivity()` before `startActivity()`** with implicit intents — app crashes if no handler found
- `android.intent.category.DEFAULT` is required in intent filter for implicit intents
- `ACTION_SEND` in intent filter: action name format = `"android.intent.action."` + action name (minus `ACTION_` prefix)
- `singleTop` only reuses if instance is at **TOP** of stack; creates new if anywhere else
- `onNewIntent()` must call `setIntent(intent)` so `getIntent()` returns the new intent
- Intent flags take **precedence** over `launchMode` attribute in case of conflict
- Multiple `<intent-filter>` elements per activity = OR logic (intent only needs to match ONE filter)
- Within one filter: intent must pass ALL elements (action, category, data)

---

## Quick Revision Bullets
- Implicit intent: action + (optional) category + (optional) data type; system finds handler
- Always `resolveActivity(getPackageManager())` before `startActivity()` with implicit intents
- Intent filter must include `android.intent.category.DEFAULT` to receive implicit intents
- `createChooser(intent, title)` forces chooser even if user has a default app
- ShareCompat.IntentBuilder makes sharing easier and backward-compatible
- Launch modes: standard (default), singleTop, singleTask, singleInstance
- `singleTop` reuses only if at top of stack; `onNewIntent()` called
- Intent flags: `FLAG_ACTIVITY_NEW_TASK`, `FLAG_ACTIVITY_SINGLE_TOP`, `FLAG_ACTIVITY_CLEAR_TOP`
---
---

# CHAPTER 3.1: The Android Studio Debugger

## Concept Overview
Debugging is the process of finding and fixing errors in code. Android Studio provides a powerful integrated debugger. Key tools: breakpoints, step execution, variable inspection, watches, expression evaluation.

---

## Theory & Logic

### Running the Debugger

**Starting in debug mode:**
- Click **Debug** icon (bug icon) in toolbar
- Android Studio builds APK, installs, runs, and opens Debug window

**Attaching to running app:**
1. Run > Attach debugger to Android process (or click Attach icon in toolbar)
2. Choose Process dialog → select app process → OK

**Stopping:**
- Run > Resume Program (or Resume icon) to continue
- Run > Stop (or Stop icon) to end debugging

### Breakpoints

**Adding a breakpoint:**
- Click in the **left gutter** next to line numbers (red dot appears)
- Or: Run > Toggle Line Breakpoint (Ctrl+F8 / Cmd+F8 on Mac)
- If app is running, breakpoints can be added without rebuilding

**Viewing/configuring breakpoints:**
- Click **View Breakpoints** icon in debugger window
- Left pane: all breakpoints with checkboxes (enable/disable)
- Exception Breakpoints: stops on any exception

**Types of breakpoints:**
- Regular: always stops execution when reached
- **Conditional**: stops only if a boolean expression is true

```java
// Conditional breakpoint example:
// Right-click breakpoint → Condition field → enter Java expression
// Example condition: mCount > 5 && itemPosition == 3
```

**Muting breakpoints:** Click "Mute Breakpoints" icon → all breakpoints temporarily disabled (without removing them)

### Stepping Through Code

| Action | Keyboard | What it does |
|--------|----------|-------------|
| **Step Over** | F8 | Execute next line; stay in current class/method |
| **Step Into** | F7 | Jump INTO the method being called |
| **Step Out** | Shift+F8 | Finish current method; return to calling location |
| **Resume** | F9 | Continue normal execution |

### Viewing Execution Stack Frames
- **Frames view** shows the execution stack (call chain)
- Most recent frame at top
- Click a frame → opens its source file, highlights the line → Variables/Watches update

```
Frame Stack (example):
  calculateTotal()  ← current (most recent)
  onButtonClick()
  MainActivity.onCreate()
```

### Inspecting and Modifying Variables
- **Variables view** shows all variables in current stack frame
- Expand objects/arrays to see fields
- **Right-click** variable → Set Value (or F2) to modify at runtime

### Setting Watches
- Watches persist between debugging sessions (unlike Variables view)
- Click **+** in Watches pane → type variable name or expression → Enter
- Useful for frequently accessed variables or state tracking

### Evaluating Expressions
- Run > Evaluate Expression (or the icon)
- Enter any Java expression, including method calls
- Result shown based on current app state
- **Warning**: Evaluating expressions can change the running state of your app

### Other Debugging Tools

| Tool | Purpose |
|------|---------|
| **Logcat (Log class)** | Write messages to the Android system log |
| **Tracing** | `Debug.startMethodTracing()` / `Debug.stopMethodTracing()` — creates trace files |
| **Android Debug Bridge (ADB)** | Command-line tool to communicate with device/emulator |
| **DDMS** | Port-forwarding, screen capture, thread/heap info, logcat, SMS spoofing |
| **CPU/Memory Monitors** | Visualize app performance |

### Trace Logging

```java
// Start tracing in onCreate()
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Debug.startMethodTracing("myTrace");  // creates myTrace.trace file
    setContentView(R.layout.activity_main);
}

// Stop tracing in onDestroy()
@Override
protected void onDestroy() {
    super.onDestroy();
    Debug.stopMethodTracing();
}
```

### Before Release: Remove All Debug Code
- Remove all `Log.d()` and `Log.e()` calls
- Remove Toast messages
- Disable debugging in manifest: `android:debuggable="false"` or remove the attribute
- Remove all `startMethodTracing()` and `stopMethodTracing()` calls

---

## Common Exam Traps / Edge Cases
- Conditional breakpoints use **Java boolean expressions** — can reference variable names
- "Muting" breakpoints disables without removing them; you keep conditions/settings
- `onDestroy()` is NOT guaranteed to be called — don't put tracing stop only there
- Variables view changes don't persist (ephemeral); Watches persist across sessions
- Evaluating expressions CAN change app state — be careful
- Remove all debug code before release (Log statements, debug flag, tracing)

---

## Quick Revision Bullets
- Debug icon → builds/installs/runs in debug mode
- Breakpoints: red dot in gutter; conditional with boolean expression
- Step Over (F8): stay in method; Step Into (F7): enter method; Step Out (Shift+F8): finish method
- Frames view = call stack (most recent on top)
- Variables view: inspect/modify at runtime; Watches: persistent across sessions
- Evaluate Expression: test any Java expression; can change app state
- Remove all debug code (Log calls, debug flag, tracing) before release

---
---

# CHAPTER 3.2: Testing Your App

## Concept Overview
Testing ensures your app works correctly in all situations. Android Studio supports **local unit tests** (run on JVM) and **instrumented tests** (run on device/emulator). Unit tests use JUnit 4.

**Test-Driven Development (TDD)**: write tests before code; tests define expected behavior.

---

## Theory & Logic

### Types of Tests

| Test Type | Runs On | Purpose | Location |
|-----------|---------|---------|----------|
| **Local Unit Tests** | JVM (fast) | Test logic that doesn't need Android framework | `src/test/java/` |
| **Instrumented Tests** | Device/Emulator | Test code that needs Android framework; UI testing | `src/androidTest/java/` |

### Android Studio Source Sets
- `main/` — app code and resources
- `test/` — local unit tests (`src/test/java/`)
- `androidTest/` — instrumented tests (`src/androidTest/java/`)

### Setting Up Testing — build.gradle Dependencies

```groovy
dependencies {
    // Required: JUnit 4 framework
    testCompile 'junit:junit:4.12'

    // Optional: Hamcrest matchers (for assertThat)
    testCompile 'org.hamcrest:hamcrest-library:1.3'

    // Optional: Mockito (for mock objects)
    testCompile 'org.mockito:mockito-core:1.10.19'
}

android {
    defaultConfig {
        // For instrumented tests with AndroidJUnitRunner
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
}
```

### Writing Unit Tests — JUnit 4

```java
@RunWith(JUnit4.class)    // specifies test runner
@SmallTest                // size annotation (small = fast, isolated test)
public class CalculatorTest {

    private Calculator mCalculator;

    @Before                // setup method, runs before EACH @Test method
    public void setUp() {
        mCalculator = new Calculator();
    }

    @Test                 // marks this as an actual test
    public void addTwoNumbers() {
        double resultAdd = mCalculator.add(1d, 1d);
        // assertThat with Hamcrest matchers (most flexible)
        assertThat(resultAdd, is(equalTo(2d)));
    }

    @Test
    public void subtractTwoNumbers() {
        double result = mCalculator.subtract(5d, 2d);
        assertThat(result, is(equalTo(3d)));
    }
}
```

**JUnit Annotations:**

| Annotation | Meaning |
|------------|---------|
| `@RunWith(JUnit4.class)` | Specifies test runner |
| `@SmallTest` | Small, fast test |
| `@MediumTest` | Medium-sized test |
| `@LargeTest` | Large/slow test |
| `@Before` | Runs before each test method (setup) |
| `@After` | Runs after each test method (teardown) |
| `@BeforeClass` | Runs once before all test methods |
| `@AfterClass` | Runs once after all test methods |
| `@Test` | Marks a test method |
| `@Ignore` | Skips this test |

**JUnit Assertion Methods:**
```java
assertEquals(expected, actual)          // tests equality
assertNotEquals(unexpected, actual)
assertTrue(condition)                   // tests boolean true
assertFalse(condition)                  // tests boolean false
assertNull(object)                      // tests for null
assertNotNull(object)                   // tests for non-null
assertThat(actual, matcher)             // flexible with Hamcrest matchers
```

**Hamcrest Matchers (used with assertThat):**
```java
assertThat(result, is(equalTo(2d)));    // result equals 2.0
assertThat(list, hasItem("hello"));     // list contains "hello"
assertThat(str, containsString("world")); // string contains substring
assertThat(num, greaterThan(5));        // number is greater than 5
```

**Best practice**: One assertion per test method — makes failures easier to debug.

### Running Tests
- Run single test: right-click test method → Run
- Run all tests in a class: right-click test file → Run
- Run all tests in a directory: right-click directory → Run tests
- Results appear in **Run window** at bottom; green bar = pass; red = fail

---

## Code: Complete Calculator Test Example

```java
package com.example.android.calculatortest;

import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.JUnit4;

import static org.hamcrest.CoreMatchers.equalTo;
import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertThat;

@RunWith(JUnit4.class)    // use JUnit4 test runner
public class CalculatorTest {

    private Calculator mCalculator;  // the object under test

    @Before
    public void setUp() throws Exception {
        // Create a fresh Calculator instance before each test
        mCalculator = new Calculator();
    }

    @Test
    public void addTwoNumbers() {
        // Act: call the method under test
        double resultAdd = mCalculator.add(1d, 1d);

        // Assert: verify the result
        // assertThat(actual, matcher) — best practice for clear failure messages
        assertThat(resultAdd, is(equalTo(2d)));
    }

    @Test
    public void addTwoNumbersNegative() {
        double resultAdd = mCalculator.add(-1d, 2d);
        assertThat(resultAdd, is(equalTo(1d)));
    }

    @Test
    public void subtractTwoNumbers() {
        double resultSub = mCalculator.sub(2d, 1d);
        assertThat(resultSub, is(equalTo(1d)));
    }

    @Test
    public void divTwoNumbers() {
        double resultDiv = mCalculator.div(32d, 2d);
        assertThat(resultDiv, is(equalTo(16d)));
    }

    @Test
    public void divByZero() {
        // Test edge case: division by zero
        double resultDiv = mCalculator.div(32d, 0d);
        // Java: 32/0.0 = Infinity (for doubles, no exception thrown)
        assertThat(resultDiv, is(equalTo(Double.POSITIVE_INFINITY)));
    }
}
```

---

## Common Exam Traps / Edge Cases
- `@Before` runs before **each** test method, not once; use `@BeforeClass` for once
- Test class files typically named `[ClassName]Test.java` — not required but convention
- One assertion per test — grouping assertions makes it hard to see which specific assertion failed
- `testCompile` for unit tests; `androidTestCompile` for instrumented tests — they're different!
- Local unit tests run on JVM (fast); instrumented tests run on device (slow)
- `assertThat(resultAdd, is(equalTo(2d)))` — note the double literal `2d` (not `2`)

---

## Quick Revision Bullets
- Two test types: local unit tests (JVM, `src/test/`) and instrumented tests (device, `src/androidTest/`)
- JUnit 4: `@RunWith`, `@Before`, `@Test`, `@After`, `@SmallTest`
- `assertThat(actual, matcher)` — most flexible; uses Hamcrest matchers
- One assertion per test method (best practice for clarity)
- `testCompile` for unit tests; `androidTestCompile` for instrumented tests in build.gradle
- Run tests: right-click test file → Run; results in Run window (green = pass)
- `@Before` runs before EACH test; `@BeforeClass` runs once before all tests

---
---

# CHAPTER 3.3: The Android Support Library

## Concept Overview
The **Android Support Library** is a set of libraries that provide backward-compatible versions of Android features, plus additional UI elements. It lets you use newer features on older devices.

---

## Theory & Logic

### Why Use the Support Library?
- **Backward compatibility**: Use features from newer Android versions on older devices
- **Additional UI elements**: RecyclerView, CardView, Fragments, FloatingActionButton
- **Different device form factors**: TV-specific (Leanback), Wearables
- **Material Design support**: via the Design Support Library
- **Other features**: Palette, Annotations, Percentage-based layouts

### Key Support Libraries

**v4 support library** — largest set of APIs:
- `v4 compat library` — Compatibility wrappers (class names contain "Compat")
- `v4 core-utils` — utility classes
- `v4 core-ui` — UI-related components
- `v4 media-compat` — media framework backport from API 21
- `v4 fragment library` — Fragment support

**v7 support library** (includes all v4):
- `v7 appcompat library` — ActionBar, Material Design UI
- `v7 cardview library` — CardView class
- `v7 gridlayout library` — GridLayout
- `v7 mediarouter library` — MediaRouter for Google Cast
- `v7 palette library` — Palette for color extraction from images
- `v7 recyclerview library` — **RecyclerView** for efficient list display
- `v7 preference library` — Preference objects for Settings

**Other libraries:**
- `v13` — Fragment support with FragmentCompat
- `v17 leanback` — TV device UI
- `Design Support Library` — Navigation drawers, FAB, Snackbars, Tabs
- `Annotations support library` — annotation metadata
- `Custom Tabs support library` — custom tabs in apps

### Version Numbers
Format: `X.Y.Z` where X = API level, Y.Z = revision.
- Example: `22.3.4` = version 3.4 for API 22
- Always use the **most recent version** compatible with your target API
- All libraries require minimum SDK of **API 9**
- Can use newer library version with older target API, but NOT vice versa

### Setting Up the Support Library

**Step 1: Download** (via SDK Manager → SDK Tools → Android Support Repository)

**Step 2: Find the dependency statement**
- Visit Support Library Features page on developer.android.com
- Find the library (e.g., Design Support Library)
- Copy: `com.android.support:design:23.3.0`

**Step 3: Add to build.gradle**

```groovy
dependencies {
    // AppCompat (v7) — includes all v4 libraries
    compile 'com.android.support:appcompat-v7:24.2.1'

    // Design Support Library (Material Design components)
    compile 'com.android.support:design:24.2.1'

    // RecyclerView
    compile 'com.android.support:recyclerview-v7:24.2.1'

    // CardView
    compile 'com.android.support:cardview-v7:24.2.1'

    // Palette
    compile 'com.android.support:palette-v7:24.2.1'
}
```

Then **Sync Now** to apply changes.

### Using Support Library APIs

**In Java:** Use the support package names:
```java
// Use support library version (preferred)
import android.support.v7.app.ActionBar;

// NOT the framework version (unless you only target API 11+)
import android.app.ActionBar;
```

**In XML layouts:** Use fully-qualified class names:
```xml
<android.support.design.widget.CoordinatorLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
</android.support.design.widget.CoordinatorLayout>
```

### Checking System Versions

```java
private void setUpActionBar() {
    // Check Android version before using version-specific APIs
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB) {
        ActionBar actionBar = getActionBar();
        actionBar.setDisplayHomeAsUpEnabled(true);
    } else {
        // do something else for older versions
    }
}
```

---

## Common Exam Traps / Edge Cases
- Support library ≠ Testing Support Library — they are DIFFERENT packages
- All support libraries require minimum SDK of **API 9**
- If using v7 + v13 + v14, your minimum API must be at least **14** (the largest number)
- Support library classes often have "Compat" in the name (e.g., `ActivityCompat`)
- In XML, support library views need **fully-qualified** class name (e.g., `android.support.design.widget.FloatingActionButton`)
- When in doubt between support class and framework class — **choose the support class**

---

## Quick Revision Bullets
- Support Library = set of libraries for backward compat + extra UI elements
- v4 = largest set; v7 includes all v4; all require min SDK API 9
- Design Support Library: FAB, Snackbars, Navigation Drawer, Tabs
- Add to build.gradle `dependencies {}` block, then Sync
- Support library classes use `android.support.*` packages; XML uses fully-qualified names
- "Compat" in class name = backward-compatible wrapper (e.g., ActivityCompat)
- Use `Build.VERSION.SDK_INT >= Build.VERSION_CODES.CONSTANT` to check Android version

---
---

# CHAPTER 4.1: User Input Controls

## Concept Overview
Android provides many **input controls** for user interaction: buttons, text fields, checkboxes, radio buttons, toggle buttons, spinners, and more. All input controls are based on the **View** class. **Focus** determines which view receives user input.

---

## Theory & Logic

### Input Controls and View Focus
- **Focus** = which view is currently selected to receive input
- **Focusable** = whether a view can gain focus from an input device (keyboard/d-pad)
- **Clickable** = whether a view can respond to touch/click events
- In "touch mode" (smartphones/tablets), only views with `isFocusableInTouchMode()=true` can gain focus (e.g., EditText)

**Controlling focus order in XML:**
```xml
<LinearLayout android:orientation="vertical">
    <Button android:id="@+id/top"
        android:nextFocusUp="@+id/bottom"   <!-- override focus direction -->
        android:nextFocusDown="@+id/bottom" />
    <Button android:id="@+id/bottom"
        android:nextFocusUp="@+id/top"
        android:nextFocusDown="@+id/top" />
</LinearLayout>
```

**Focus methods:**
```java
Activity.getCurrentFocus()           // which view has focus
ViewGroup.getFocusedChild()          // focused child of a ViewGroup
view.findFocus()                     // view in hierarchy that has focus
view.requestFocus()                  // programmatically set focus
view.setFocusable(boolean)           // change focusability
view.setOnFocusChangeListener(...)   // listener for focus changes
```

### Buttons

**Raised Button (text only):**
```xml
<Button
    android:id="@+id/button_send"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_send"
    android:onClick="sendMessage" />   <!-- calls sendMessage() in activity -->
```

**Raised Button (icon + text):**
```xml
<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_text"
    android:drawableLeft="@drawable/button_icon" />
```

**Image Button (icon only):**
```xml
<ImageButton
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/button_icon" />
```

**Flat (Borderless) Button:**
```xml
<Button
    android:id="@+id/button_send"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_send"
    android:onClick="sendMessage"
    style="?android:attr/borderlessButtonStyle" />   <!-- flat style -->
```

**Floating Action Button (FAB):**
```xml
<!-- Requires: compile 'com.android.support:design:23.4.0' -->
<android.support.design.widget.FloatingActionButton
    android:id="@+id/fab"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="bottom|end"    <!-- position in layout -->
    android:layout_margin="@dimen/fab_margin"
    android:src="@drawable/ic_fab_chat_button_white"
    app:fabSize="normal"                   <!-- normal (56dp) or mini (40dp) -->
    app:fabSize="mini" />
```

**FAB rules:**
- Use only for the **primary action** on a screen
- Only **one FAB** per screen recommended
- Default size: 56x56 dp (normal); mini: 40x40 dp

### Responding to Button Clicks

**Method 1: android:onClick in XML (simplest)**
```xml
<Button android:onClick="sendMessage" ... />
```
```java
// In activity — MUST be public, return void, take View parameter
public void sendMessage(View view) {
    // handle click
}
```

**Method 2: Listener Design Pattern (programmatic)**
```java
// Step 1: Get the button
Button button = (Button) findViewById(R.id.button_send);

// Step 2: Create and register OnClickListener
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // handle click
    }
});
```

**Lambda version (Java 8+):**
```java
button.setOnClickListener(v -> {
    // handle click
});
```

**Other Event Listeners:**

| Listener | Callback | When called |
|----------|----------|-------------|
| `View.OnClickListener` | `onClick(View)` | Touch + release on view |
| `View.OnLongClickListener` | `onLongClick(View)` → boolean | Long press; return true if consumed |
| `View.OnTouchListener` | `onTouch(View, MotionEvent)` → boolean | Any touch contact |
| `View.OnFocusChangeListener` | `onFocusChange(View, boolean)` | Focus gained/lost |
| `View.OnKeyListener` | `onKey(View, int, KeyEvent)` → boolean | Hardware key press |

### Checkboxes

```xml
<LinearLayout android:orientation="vertical">
    <CheckBox android:id="@+id/checkbox1_chocolate"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/chocolate_syrup" />
    <CheckBox android:id="@+id/checkbox2_sprinkles"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/sprinkles" />
</LinearLayout>
<Button android:text="@string/submit" android:onClick="onSubmit" />
```

```java
public void onSubmit(View view) {
    StringBuffer toppings = new StringBuffer();

    // Check each checkbox independently
    if (((CheckBox) findViewById(R.id.checkbox1_chocolate)).isChecked()) {
        toppings.append(getString(R.string.chocolate_syrup_text));
    }
    if (((CheckBox) findViewById(R.id.checkbox2_sprinkles)).isChecked()) {
        toppings.append(getString(R.string.sprinkles_text));
    }
}
```

**Key points:** Each checkbox is independent; `isChecked()` returns boolean.

### Radio Buttons

```xml
<RadioGroup
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">

    <RadioButton android:id="@+id/sameday"
        android:text="@string/same_day"
        android:onClick="onRadioButtonClicked" />

    <RadioButton android:id="@+id/nextday"
        android:text="@string/next_day"
        android:onClick="onRadioButtonClicked" />

    <RadioButton android:id="@+id/pickup"
        android:text="@string/pick_up"
        android:onClick="onRadioButtonClicked" />
</RadioGroup>
```

```java
public void onRadioButtonClicked(View view) {
    boolean checked = ((RadioButton) view).isChecked();

    switch(view.getId()) {
        case R.id.sameday:
            if (checked) { /* Same day service */ }
            break;
        case R.id.nextday:
            if (checked) { /* Next day delivery */ }
            break;
        case R.id.pickup:
            if (checked) { /* Pick up */ }
            break;
    }
}
```

**Key points:** RadioButtons in RadioGroup are mutually exclusive — checking one unchecks all others.

### Toggle Buttons and Switches

**ToggleButton:**
```xml
<ToggleButton
    android:id="@+id/my_toggle"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:onClick="onToggleClick" />
```

```java
public void onToggleClick(View view) {
    ToggleButton toggle = (ToggleButton) findViewById(R.id.my_toggle);
    toggle.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
        @Override
        public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
            if (isChecked) {
                // Toggle ON
            } else {
                // Toggle OFF
            }
        }
    });
}
```

**Switch (similar to ToggleButton):**
```xml
<Switch
    android:id="@+id/my_switch"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/turn_on_or_off"  <!-- text appears to LEFT of switch -->
    android:onClick="onSwitchClick" />
```

Both ToggleButton and Switch extend **CompoundButton**. Can be set programmatically with `setChecked(boolean)` — note: won't trigger `onClick()`.

### Spinners (Dropdown)

```xml
<Spinner
    android:id="@+id/label_spinner"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```

```xml
<!-- In res/values/strings.xml -->
<string-array name="labels_array">
    <item>Home</item>
    <item>Work</item>
    <item>Mobile</item>
    <item>Other</item>
</string-array>
```

```java
// In onCreate():
Spinner spinner = (Spinner) findViewById(R.id.label_spinner);
if (spinner != null) {
    spinner.setOnItemSelectedListener(this);  // activity implements AdapterView.OnItemSelectedListener
}

// Create adapter from the string array
ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(
    this,                              // context
    R.array.labels_array,              // the array resource
    android.R.layout.simple_spinner_item  // layout for each item
);
// Set dropdown layout
adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
// Connect adapter to spinner
if (spinner != null) {
    spinner.setAdapter(adapter);
}
```

**Activity must implement OnItemSelectedListener:**
```java
public class MainActivity extends AppCompatActivity
        implements AdapterView.OnItemSelectedListener {

    @Override
    public void onItemSelected(AdapterView<?> adapterView, View view, int pos, long id) {
        // pos = position of selected item
        String spinner_item = adapterView.getItemAtPosition(pos).toString();
        // use the selected item
    }

    @Override
    public void onNothingSelected(AdapterView<?> adapterView) {
        // do nothing, or provide default behavior
    }
}
```

**Adapter Pattern:** The adapter acts as a bridge between data (the array) and the UI (the Spinner). It creates a view for each item in the data set.

### Text Input (EditText)

```xml
<EditText
    android:id="@+id/editText_main"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:maxLines="1"
    android:maxLength="5"
    android:hint="@string/enter_message"    <!-- placeholder text -->
    android:inputType="text"                <!-- keyboard type -->
    android:textColorHighlight="#7cff88" />  <!-- selected text background -->
```

**`android:inputType` values:**

| Value | Effect |
|-------|--------|
| `textCapSentences` | Capitalizes start of sentence |
| `textAutoCorrect` | Enables spell check suggestions |
| `textPassword` | Each char becomes a dot |
| `textEmailAddress` | Email keyboard (@ key prominent) |
| `phone` | Numeric phone keypad |
| `number` | Numeric keypad |

**Combining inputTypes:**
```xml
android:inputType="textAutoCorrect|textCapSentences"  <!-- pipe = bitwise OR -->
```

**Getting input from EditText:**
```java
EditText editText = (EditText) findViewById(R.id.editText_main);
String showString = editText.getText().toString();
// Convert to integer if needed:
int number = Integer.valueOf(editText.getText().toString());
```

**Changing the "Action" key (Return/Enter):**
```java
EditText editText = (EditText) findViewById(R.id.phone_number);
editText.setOnEditorActionListener(new TextView.OnEditorActionListener() {
    @Override
    public boolean onEditorAction(TextView textView, int actionId, KeyEvent keyEvent) {
        boolean handled = false;
        if (actionId == EditorInfo.IME_ACTION_SEND) {
            dialNumber();       // perform the action
            handled = true;     // return true = event consumed
        }
        return handled;
    }
});
```

### Dialogs

```java
// Build an AlertDialog
AlertDialog.Builder myAlertBuilder = new AlertDialog.Builder(MainActivity.this);
myAlertBuilder.setTitle(R.string.alert_title);
myAlertBuilder.setMessage(R.string.alert_message);

// Positive button (e.g., "OK")
myAlertBuilder.setPositiveButton("OK", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        // User clicked OK
    }
});

// Negative button (e.g., "Cancel")
myAlertBuilder.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        // User clicked Cancel
    }
});

// Optional: Neutral button (between positive and negative)
myAlertBuilder.setNeutralButton("Remind me later", ...);

// Display the dialog
AlertDialog alertDialog = myAlertBuilder.create();
alertDialog.show();
```

**AlertDialog regions:**
1. **Title** (optional) — use only for high-risk situations
2. **Content area** — message, list, or custom layout
3. **Action buttons** — max 3: positive, negative, neutral

**Builder Design Pattern:** AlertDialog.Builder makes constructing complex objects with many optional attributes clean and readable.

### Date and Time Pickers

```java
// DatePickerFragment.java
public class DatePickerFragment extends DialogFragment
        implements DatePickerDialog.OnDateSetListener {

    @Override
    public Dialog onCreateDialog(Bundle savedInstanceState) {
        // Set default date to today
        final Calendar c = Calendar.getInstance();
        int year = c.get(Calendar.YEAR);
        int month = c.get(Calendar.MONTH);   // 0-indexed (January = 0)
        int day = c.get(Calendar.DAY_OF_MONTH);

        return new DatePickerDialog(getActivity(), this, year, month, day);
    }

    @Override
    public void onDateSet(DatePicker view, int year, int month, int day) {
        // User has selected a date; pass to activity
        MainActivity activity = (MainActivity) getActivity();
        activity.processDatePickerResult(year, month, day);
    }
}

// In MainActivity:
public void showDatePickerDialog(View v) {
    DialogFragment newFragment = new DatePickerFragment();
    newFragment.show(getSupportFragmentManager(), "datePicker");
}

public void processDatePickerResult(int year, int month, int day) {
    // month is 0-indexed, add 1 for display
    String month_string = Integer.toString(month + 1);
    String day_string = Integer.toString(day);
    String year_string = Integer.toString(year);
    String dateMessage = month_string + "/" + day_string + "/" + year_string;
    Toast.makeText(this, getString(R.string.date) + dateMessage, Toast.LENGTH_SHORT).show();
}
```

**CRITICAL:** Calendar.MONTH is **0-indexed** (January = 0, December = 11). Always add 1 for display!

### Gesture Detection

```java
public class MainActivity extends Activity {
    private GestureDetectorCompat mDetector;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // Create GestureDetector with a listener
        mDetector = new GestureDetectorCompat(this, new MyGestureListener());
    }

    // Forward touch events to detector
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        this.mDetector.onTouchEvent(event);
        return super.onTouchEvent(event);
    }
}

// Gesture listener class
class MyGestureListener extends GestureDetector.SimpleOnGestureListener {
    private static final String DEBUG_TAG = "Gestures";

    @Override
    public boolean onDown(MotionEvent event) {
        Log.d(DEBUG_TAG, "onDown: " + event.toString());
        return true;    // must return true to receive subsequent events
    }

    @Override
    public boolean onFling(MotionEvent event1, MotionEvent event2,
                            float velocityX, float velocityY) {
        Log.d(DEBUG_TAG, "onFling: " + event1.toString() + event2.toString());
        return true;
    }
}
```

**MotionEvent actions:**
- `ACTION_DOWN` — finger touches screen
- `ACTION_MOVE` — finger moves
- `ACTION_UP` — finger lifts
- `ACTION_CANCEL` — gesture cancelled
- `ACTION_POINTER_DOWN` / `ACTION_POINTER_UP` — additional fingers

---

## Common Exam Traps / Edge Cases
- RadioButtons must be inside a **RadioGroup** for mutual exclusivity to work
- Calendar.MONTH is **0-indexed** — always add 1 for display
- ToggleButton/Switch `android:text` attribute is NOT the "ON/OFF" label — toggle always shows ON/OFF; text is a separate label (use TextView)
- `setChecked(boolean)` on toggle/switch does NOT trigger `onClick()` callback
- `onLongClick()` returns boolean — return `true` if event consumed, `false` to pass it on
- `resolveActivity()` must be called before `startActivity()` for implicit intents
- Spinner's `onNothingSelected()` MUST be implemented (interface requirement)

---

## Quick Revision Bullets
- All input controls extend View; focus determines which receives keyboard input
- Button types: raised (default), flat (borderless), ImageButton (icon), FAB (circular, primary action)
- Click listeners: android:onClick (XML) or setOnClickListener() (programmatic)
- Checkboxes: multiple selection; RadioButtons in RadioGroup: mutually exclusive
- ToggleButton/Switch: two-state; use OnCheckedChangeListener
- Spinner: needs ArrayAdapter + OnItemSelectedListener (onItemSelected + onNothingSelected)
- EditText: `android:inputType` controls keyboard type; `getText().toString()` to get value
- AlertDialog.Builder: setTitle, setMessage, setPositiveButton, setNegativeButton → show()
- Calendar.MONTH is 0-indexed — add 1 for human-readable display

---
---

# CHAPTER 4.2: Menus

## Concept Overview
Android provides three types of menus: **Options Menu** (in app bar), **Context Menu** (floating or action bar on long-click), and **Popup Menu** (anchored to a view). All use XML menu resource files and the **resource-inflate design pattern**.

---

## Theory & Logic

### Menu Types

| Type | Trigger | Appears |
|------|---------|---------|
| Options Menu | App bar (action bar) | Top of screen in app bar / overflow |
| Context Menu (floating) | Long-click on view | Floating list near the view |
| Contextual Action Bar | Long-click on view | Top of screen, overlaying app bar |
| Popup Menu | Click on a view (anchor) | Below or above anchor view |

### Options Menu / App Bar

**Setup steps:**
1. Add support libraries (appcompat, design)
2. Use NoActionBar theme + add styles
3. Add AppBarLayout + Toolbar to layout
4. Set up app bar in activity code
5. Create XML menu resource
6. Override `onCreateOptionsMenu()` to inflate it
7. Handle clicks in `onOptionsItemSelected()`

**Layout with Toolbar:**
```xml
<android.support.design.widget.CoordinatorLayout ... >

    <android.support.design.widget.AppBarLayout ... >
        <android.support.v7.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            app:popupTheme="@style/AppTheme.PopupOverlay" />
    </android.support.design.widget.AppBarLayout>

    <!-- Content layout needs scroll behavior -->
    <RelativeLayout
        app:layout_behavior="@string/appbar_scrolling_view_behavior"
        ... >
        <!-- main content goes here -->
    </RelativeLayout>
</android.support.design.widget.CoordinatorLayout>
```

**Activity code:**
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
    setSupportActionBar(toolbar);   // makes Toolbar the app bar
}
```

**XML Menu Resource (res/menu/menu_main.xml):**
```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <item
        android:id="@+id/action_order"
        android:icon="@drawable/ic_order_white"
        android:orderInCategory="10"             <!-- lower = higher priority -->
        android:title="@string/action_order"
        app:showAsAction="ifRoom" />             <!-- ifRoom, always, never, withText -->

    <item
        android:id="@+id/action_status"
        android:orderInCategory="20"
        android:title="@string/action_status"
        app:showAsAction="never" />              <!-- always in overflow -->

    <item
        android:id="@+id/action_settings"
        android:title="@string/settings"
        app:showAsAction="never" />
</menu>
```

**`app:showAsAction` values:**
- `always` — always show as icon in app bar (use sparingly)
- `ifRoom` — show as icon if space available; otherwise overflow
- `never` — always in overflow menu
- `withText` — show both icon and title text

**Inflating the menu:**
```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main, menu);
    return true;  // return true to show the menu
}
```

**Handling menu item clicks:**
```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case R.id.action_order:
            showOrder();         // call your method
            return true;
        case R.id.action_status:
            showStatus();
            return true;
        case R.id.action_settings:
            // go to settings
            return true;
        default:
            return super.onOptionsItemSelected(item);  // default handling
    }
}
```

### Floating Context Menu

```java
// Step 1: Register view for context menu (in onCreate)
TextView article_text = (TextView) findViewById(R.id.article);
registerForContextMenu(article_text);

// Step 2: Inflate the menu
@Override
public void onCreateContextMenu(ContextMenu menu, View v,
        ContextMenu.ContextMenuInfo menuInfo) {
    super.onCreateContextMenu(menu, v, menuInfo);
    MenuInflater inflater = getMenuInflater();
    inflater.inflate(R.menu.menu_context, menu);
}

// Step 3: Handle click
@Override
public boolean onContextItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case R.id.context_edit:
            editNote();
            return true;
        case R.id.context_share:
            shareNote();
            return true;
        default:
            return super.onContextItemSelected(item);
    }
}
```

### Contextual Action Bar

```java
// Declare member variable
private ActionMode mActionMode;

// In onCreate, set long click listener
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    View articleView = findViewById(R.id.article);
    articleView.setOnLongClickListener(new View.OnLongClickListener() {
        @Override
        public boolean onLongClick(View view) {
            if (mActionMode != null) return false;  // don't recreate if already active

            mActionMode = MainActivity.this.startActionMode(mActionModeCallback);
            view.setSelected(true);
            return true;    // event consumed
        }
    });
}

// ActionMode.Callback implementation
public ActionMode.Callback mActionModeCallback = new ActionMode.Callback() {

    @Override
    public boolean onCreateActionMode(ActionMode mode, Menu menu) {
        // Inflate the contextual action bar menu
        MenuInflater inflater = mode.getMenuInflater();
        inflater.inflate(R.menu.menu_context, menu);
        return true;
    }

    @Override
    public boolean onPrepareActionMode(ActionMode mode, Menu menu) {
        return false;  // return false if nothing changed
    }

    @Override
    public boolean onActionItemClicked(ActionMode mode, MenuItem item) {
        switch (item.getItemId()) {
            case R.id.context_edit:
                editNote();
                mode.finish();  // close the action bar
                return true;
            case R.id.context_share:
                shareNote();
                mode.finish();
                return true;
            default:
                return false;
        }
    }

    @Override
    public void onDestroyActionMode(ActionMode mode) {
        mActionMode = null;  // reset reference
    }
};
```

---

## Common Exam Traps / Edge Cases
- Options menu is created once with `onCreateOptionsMenu()`; context menu is created each time with `onCreateContextMenu()`
- For context menu to work, must call `registerForContextMenu(view)` first
- Context menu XML files DON'T need `app:showAsAction` (there's no action bar)
- Contextual action bar: check `if (mActionMode != null) return false` to prevent duplicate action bars
- `mode.finish()` closes the contextual action bar after user selects an action
- `app:showAsAction` uses `app:` namespace, NOT `android:` — important for compatibility
- `orderInCategory`: lower number = appears FIRST/higher in menu

---

## Quick Revision Bullets
- Three menu types: Options (app bar), Context (long-click), Popup (anchored to view)
- All menus use XML resource files in `res/menu/`; use `MenuInflater.inflate()` to load
- Options menu: `onCreateOptionsMenu()` inflates; `onOptionsItemSelected()` handles clicks
- Context (floating): `registerForContextMenu(view)`, `onCreateContextMenu()`, `onContextItemSelected()`
- Contextual action bar: `setOnLongClickListener` → `startActionMode()` + `ActionMode.Callback`
- `app:showAsAction`: `always`, `ifRoom`, `never`, `withText`
- `android:orderInCategory`: lower number = higher priority / appears first

---
---

# CHAPTER 4.4: RecyclerView

## Concept Overview
**RecyclerView** is a more advanced and flexible version of ListView for displaying scrolling lists of data. It uses the **Adapter Pattern** (data → view) and the **ViewHolder Pattern** (reuse views). It **recycles** views that scroll off screen instead of creating new ones.

**Mental model:** RecyclerView is like an airport moving walkway with only 10 visible seats. As passengers (data) scroll off one end, the seats are moved back to the other end for the next passengers.

---

## Theory & Logic

### RecyclerView vs. ScrollView
- **ScrollView**: loads ALL views into memory; good for static text
- **RecyclerView**: only loads visible views; recycles them as user scrolls; good for large/dynamic data sets
- RecyclerView requires a **LayoutManager** to arrange items

### RecyclerView Components

| Component | Role |
|-----------|------|
| `RecyclerView` | The view that displays items |
| `RecyclerView.Adapter` | Connects data to list item views |
| `RecyclerView.ViewHolder` | Caches view references for each item |
| `RecyclerView.LayoutManager` | Arranges items (linear, grid, etc.) |

### Implementation Steps

**Step 1: Add dependency**
```groovy
// In build.gradle
compile 'com.android.support:recyclerview-v7:24.2.1'
```

**Step 2: Add RecyclerView to layout**
```xml
<!-- In activity_main.xml -->
<android.support.v7.widget.RecyclerView
    android:id="@+id/recyclerview"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

**Step 3: Create item layout** (res/layout/wordlist_item.xml)
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="6dp">

    <TextView
        android:id="@+id/word"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="20sp" />
</LinearLayout>
```

**Step 4: Create the Adapter + ViewHolder**
```java
public class WordListAdapter
        extends RecyclerView.Adapter<WordListAdapter.WordViewHolder> {

    private final Context mContext;        // for inflating layouts
    private LinkedList<String> mWordList;  // the data

    // Constructor
    public WordListAdapter(Context context, LinkedList<String> wordList) {
        mContext = context;
        mWordList = wordList;
    }

    // Called when RecyclerView needs a new ViewHolder
    // INFLATES a new view from the item layout XML
    @Override
    public WordViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        return new WordViewHolder(
            LayoutInflater.from(mContext).inflate(R.layout.wordlist_item, parent, false),
            this
        );
    }

    // Called to BIND data to an existing ViewHolder
    // This is where you set data from your list into the views
    @Override
    public void onBindViewHolder(WordViewHolder holder, int position) {
        // Get the word at this position
        String mCurrent = mWordList.get(position);
        // Set it on the TextView in the ViewHolder
        holder.wordItemView.setText(mCurrent);
    }

    // Returns the total number of items in the data set
    @Override
    public int getItemCount() {
        return mWordList.size();  // RecyclerView uses this to know how many items
    }

    // --- INNER CLASS: ViewHolder ---
    // Holds references to the views in each item view
    // Avoids calling findViewById() repeatedly (expensive)
    class WordViewHolder extends RecyclerView.ViewHolder
            implements View.OnClickListener {

        public final TextView wordItemView;   // the TextView for the word
        final WordListAdapter mAdapter;       // reference to adapter for callbacks

        public WordViewHolder(View itemView, WordListAdapter adapter) {
            super(itemView);
            wordItemView = (TextView) itemView.findViewById(R.id.word);
            this.mAdapter = adapter;
            itemView.setOnClickListener(this);  // register click listener
        }

        @Override
        public void onClick(View v) {
            // Handle click — update the text to show it was clicked
            wordItemView.setText("Clicked! " + wordItemView.getText());
        }
    }
}
```

**Step 5: Set up RecyclerView in Activity**
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // Create some data
    LinkedList<String> mWordList = new LinkedList<>();
    for (int i = 0; i < 20; i++) {
        mWordList.addLast("Word " + i);
    }

    // Step 1: Get a handle to the RecyclerView
    RecyclerView mRecyclerView = (RecyclerView) findViewById(R.id.recyclerview);

    // Step 2: Create an adapter with the data
    WordListAdapter mAdapter = new WordListAdapter(this, mWordList);

    // Step 3: Connect the adapter to the RecyclerView
    mRecyclerView.setAdapter(mAdapter);

    // Step 4: Set a LayoutManager (LinearLayoutManager for vertical list)
    mRecyclerView.setLayoutManager(new LinearLayoutManager(this));
}
```

### RecyclerView Lifecycle (How it works)

```
Data list: ["Word 0", "Word 1", ..., "Word 19"]
Screen shows 7 items at once.

1. RecyclerView asks Adapter: how many items? → getItemCount() = 20
2. For each visible item:
   a. onCreateViewHolder() → inflate item layout, create ViewHolder
   b. onBindViewHolder(holder, 0) → set "Word 0" on holder's TextView

3. User scrolls down:
   a. "Word 0" scrolls off top
   b. RecyclerView RECYCLES the ViewHolder
   c. onBindViewHolder(recycledHolder, 7) → set "Word 7" on SAME ViewHolder
   d. RecyclerView doesn't create a new ViewHolder!
```

**This is the key efficiency: `onCreateViewHolder()` is called few times; `onBindViewHolder()` is called for each item that becomes visible.**

---

## Common Exam Traps / Edge Cases
- `onCreateViewHolder()` inflates a new view; `onBindViewHolder()` binds data to existing view
- ViewHolder caches `findViewById()` calls — avoids calling it repeatedly as user scrolls
- `getItemCount()` MUST return the correct count; RecyclerView won't show more items
- RecyclerView needs three things: Adapter, LayoutManager, and data
- For grid layout instead of linear: use `GridLayoutManager` instead of `LinearLayoutManager`
- To add items dynamically: call `mAdapter.notifyDataSetChanged()` or `notifyItemInserted(pos)` after modifying data
- Click listeners on items are attached in `ViewHolder` constructor (`itemView.setOnClickListener(this)`) not in `onBindViewHolder`

---

## Quick Revision Bullets
- RecyclerView = efficient scrolling list; recycles off-screen views
- Three required components: RecyclerView.Adapter, RecyclerView.ViewHolder, RecyclerView.LayoutManager
- `onCreateViewHolder()` = inflate layout, create ViewHolder (called few times)
- `onBindViewHolder()` = set data on ViewHolder's views (called for every visible item)
- `getItemCount()` = total number of data items
- ViewHolder pattern: caches view references to avoid repeated `findViewById()` calls
- LinearLayoutManager for vertical lists; GridLayoutManager for grid; StaggeredGridLayoutManager for staggered
- Add dependency: `compile 'com.android.support:recyclerview-v7:X.X.X'`
---
---

# CHAPTER 5.1: Drawables, Styles, and Themes

## Concept Overview
A **Drawable** is a graphic that can be drawn to the screen. **Styles** apply to individual Views. **Themes** apply to entire Activities or Applications. Together they enable consistent, attractive UI without duplicating attribute definitions.

---

## Theory & Logic

### Drawable Types

| Type | Description | Extension |
|------|-------------|-----------|
| Image files | Bitmap images | .webp (preferred), .png (preferred), .jpg |
| Nine-patch | Stretchable PNG with defined stretchable regions | .9.png |
| Layer list | Multiple drawables stacked on each other | XML |
| Shape drawable | Rectangle, oval, line, or ring defined in XML | XML |
| State list | Different image per widget state | XML |
| Level list | Different image per numeric level | XML |
| Transition drawable | Cross-fade between two drawables | XML |
| Vector drawable | Scalable image defined by path (API 21+) | XML |

### Using Drawables

```xml
<!-- Display an image in an ImageView -->
<ImageView
    android:id="@+id/tiles"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/birthdaycake" />
```

```java
// Get drawable programmatically
Resources res = getResources();
Drawable drawable = res.getDrawable(R.drawable.birthdaycake);
```

**Image formats (priority order):**
1. **WebP** (fully supported from Android 4.2) — best compression, 25%+ smaller than JPEG
2. **PNG** — lossless, preferred for icons
3. **JPG** — acceptable for photos
4. **GIF, BMP** — supported but discouraged

**Store images in:** `res/drawable/` or density-specific folders: `res/drawable-hdpi/`, `res/drawable-xxhdpi/`, etc.

### Nine-Patch Files (.9.png)

A nine-patch image has a **1-pixel border** defining stretchable regions — the image stretches correctly regardless of the View size.

```
[Corner]  [Stretchable horizontal]  [Corner]
[Stretchable vertical]  [Content area]  [Stretchable vertical]
[Corner]  [Stretchable horizontal]  [Corner]
```

- Save as `.9.png` in `res/drawable/`
- Create in Android Studio: right-click PNG → Create 9-Patch file → Draw 9-Patch editor
- **Android's default Button uses a 9-patch background** — that's why it stretches correctly
- Stretchable regions must be at least **2×2 pixels** in size

### Layer List Drawables

```xml
<!-- res/drawable/layered_image.xml -->
<!-- Layers drawn bottom to top; LAST item = shown on top -->
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item>
        <bitmap android:src="@drawable/android_red"
                android:gravity="center" />
    </item>
    <item android:top="10dp" android:left="10dp">
        <bitmap android:src="@drawable/android_green"
                android:gravity="center" />
    </item>
    <item android:top="20dp" android:left="20dp">
        <!-- android_blue is DRAWN LAST = appears on TOP -->
        <bitmap android:src="@drawable/android_blue"
                android:gravity="center" />
    </item>
</layer-list>
```

### Shape Drawables

```xml
<!-- res/drawable/gradient_box.xml -->
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">    <!-- rectangle | oval | line | ring -->

    <corners android:radius="8dp" />        <!-- rounded corners -->

    <gradient
        android:startColor="#000000"        <!-- black at bottom-left -->
        android:endColor="#0000dd"          <!-- blue at top-right -->
        android:angle="45"                  <!-- angle must be 0 or multiple of 45 -->
        android:type="linear" />            <!-- linear | radial | sweep -->

    <padding
        android:left="7dp"
        android:top="7dp"
        android:right="7dp"
        android:bottom="7dp" />

    <stroke                                 <!-- for "line" shape: stroke is REQUIRED -->
        android:width="2dp"
        android:color="#FF0000"
        android:dashWidth="5dp"             <!-- for dashed border -->
        android:dashGap="3dp" />

    <solid android:color="#FF0000" />      <!-- solid fill color (use instead of gradient) -->
</shape>
```

```xml
<!-- Apply shape as background -->
<TextView
    android:background="@drawable/gradient_box"
    android:layout_height="wrap_content"
    android:layout_width="wrap_content" />
```

```java
// Apply programmatically
Resources res = getResources();
Drawable shape = res.getDrawable(R.drawable.gradient_box);
TextView tv = (TextView) findViewByID(R.id.textview);
tv.setBackground(shape);
```

### State List Drawables

```xml
<!-- res/drawable/button_states.xml -->
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- Checked FIRST to LAST; first match wins (not best match!) -->
    <item android:state_pressed="true"
          android:drawable="@drawable/button_pressed" />   <!-- pressed state -->
    <item android:state_focused="true"
          android:drawable="@drawable/button_focused" />   <!-- focused state -->
    <item android:state_hovered="true"
          android:drawable="@drawable/button_focused" />   <!-- hovered state -->
    <item android:drawable="@drawable/button_normal" />    <!-- default state (last!) -->
</selector>
```

**Available state attributes:**
- `android:state_pressed` — true when being pressed
- `android:state_focused` — true when focused
- `android:state_hovered` — true when being hovered over (API 14+)
- `android:state_selected` — true when selected
- `android:state_checked` — true when checked (CheckBox, RadioButton)
- `android:state_enabled` — true when enabled

**CRITICAL:** State list is checked **top to bottom; first match wins**. Always put the default state LAST.

### Level List Drawables

```xml
<!-- res/drawable/battery_level.xml -->
<?xml version="1.0" encoding="utf-8"?>
<level-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@drawable/battery_empty" android:maxLevel="0" />
    <item android:drawable="@drawable/battery_low"   android:maxLevel="25" />
    <item android:drawable="@drawable/battery_mid"   android:maxLevel="75" />
    <item android:drawable="@drawable/battery_full"  android:maxLevel="100" />
</level-list>
```

```java
// Use setLevel() to select which drawable to show
ImageView batteryIcon = (ImageView) findViewById(R.id.battery_icon);
batteryIcon.setImageLevel(65);  // selects battery_mid (first level >= 65 is 75)
```

### Transition Drawables

```xml
<!-- res/drawable/on_off_transition.xml -->
<transition xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@drawable/on" />   <!-- first drawable -->
    <item android:drawable="@drawable/off" />  <!-- second drawable -->
</transition>
```

```java
ImageView image = (ImageView) findViewById(R.id.image);
TransitionDrawable transition = (TransitionDrawable) image.getDrawable();

// Forward: first → second (takes 1 second = 1000ms)
transition.startTransition(1000);

// Reverse: second → first
transition.reverseTransition(1000);
```

### Vector Drawables (API 21+)

```xml
<!-- res/drawable/heart.xml -->
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:height="256dp"
    android:width="256dp"
    android:viewportWidth="32"
    android:viewportHeight="32">

    <path android:fillColor="#f00"
        android:pathData="M20.5,9.5 c-1.955,0,-3.83,1.268,-4.5,3 ..." />
</vector>
```

**Advantages of vector drawables:**
- Scale without losing quality (no pixelation)
- Single file works for all screen densities → smaller APK
- Supported via `VectorDrawableCompat` down to API 7 (with Support Library)

**Creating vector drawables in Android Studio:**
- Right-click res/drawable → New → Vector Asset → import SVG or choose Material icon

---

## Styles

A **style** is a collection of attributes that define the look and format of a View. Applied to a single View.

```xml
<!-- res/values/styles.xml -->
<resources>
    <!-- Define a style -->
    <style name="CodeFont">
        <item name="android:typeface">monospace</item>
        <item name="android:textColor">#D7D6D7</item>
    </style>

    <!-- Inherit from a platform style and override -->
    <style name="GreenText" parent="@android:style/TextAppearance">
        <item name="android:textColor">#00FF00</item>
    </style>

    <!-- Inherit from own style using dot notation -->
    <!-- CodeFont.RedLarge inherits ALL of CodeFont, then overrides/adds -->
    <style name="CodeFont.RedLarge">
        <item name="android:textColor">#FF0000</item>
        <item name="android:textSize">34sp</item>
    </style>
</resources>
```

**Applying a style to a View:**
```xml
<TextView
    style="@style/CodeFont"
    android:text="@string/code_string" />
```

**Style inheritance:**
1. Via `parent` attribute: `parent="@android:style/TextAppearance"` — inherits from platform style
2. Via dot notation: `name="CodeFont.RedLarge"` — inherits from own `CodeFont` style

**Platform style examples:**
- `@android:style/TextAppearance`
- `Theme.AppCompat.Light.DarkActionBar`
- `Theme.AppCompat`
- `Theme.AppCompat.DayNight`

---

## Themes

A **theme** is applied to an entire Activity or Application, not just one View.

```xml
<!-- res/values/styles.xml -->
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <!-- Three key colors in Material Design -->
    <item name="colorPrimary">@color/colorPrimary</item>        <!-- app bar color -->
    <item name="colorPrimaryDark">@color/colorPrimaryDark</item> <!-- status bar color -->
    <item name="colorAccent">@color/colorAccent</item>           <!-- highlight color -->
</style>

<!-- NoActionBar variant (for using Toolbar instead of ActionBar) -->
<style name="AppTheme.NoActionBar">
    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
</style>
```

**Applying a theme in AndroidManifest.xml:**
```xml
<!-- Apply to entire application -->
<application android:theme="@style/AppTheme">

<!-- Apply to a specific activity -->
<activity android:theme="@android:style/Theme.Dialog">
```

**Difference: Style vs Theme:**
- Style → `style="@style/Name"` attribute in XML → applies to ONE View
- Theme → `android:theme="@style/Name"` in manifest → applies to entire Activity or App

**Platform themes (common):**
- `Theme.AppCompat.Light.DarkActionBar` — light background, dark action bar (default for new projects)
- `Theme.AppCompat` — dark background, light text
- `Theme.AppCompat.Light` — light background, dark text
- `Theme.AppCompat.DayNight` — automatically switches light/dark based on time of day

### Image Loading Libraries (Glide, Picasso)

```groovy
// Add Glide dependency
compile 'com.github.bumptech.glide:glide:n.n.n'
```

```java
// Load image from URL into ImageView using Glide
ImageView imageView = (ImageView) findViewById(R.id.my_image_view);
Glide.with(this)        // context
     .load("URL")       // image URL (or File, resource ID, etc.)
     .into(imageView);  // target ImageView
```

**Glide features:** fetching, decoding, displaying images and animated GIFs; placeholder images; cross-fade animations; automatic caching.

---

## Common Exam Traps / Edge Cases
- State list is checked **top to bottom; first match wins** — always put default state LAST
- Nine-patch stretchable regions must be at least **2×2 pixels**
- Layer list: **last item is drawn on top** (like drawing on a canvas — last painted covers earlier)
- Shape drawable: gradient angle must be 0 or a **multiple of 45** degrees
- For `line` shape: `<stroke>` element is REQUIRED
- Style = applies to View (style attribute); Theme = applies to Activity/App (android:theme attribute)
- Dot notation inheritance `"CodeFont.RedLarge"` = inherits from `CodeFont`; parent attribute for platform styles
- Vector drawables available from API 21+; use VectorDrawableCompat for older devices

---

## Quick Revision Bullets
- Drawable = graphic drawable to screen; 8 types: image, 9-patch, layer list, shape, state list, level list, transition, vector
- Preferred image formats: WebP > PNG > JPG
- 9-patch: stretchable PNG with defined regions; must be `.9.png`; button backgrounds use 9-patch
- State list: order matters — first match wins; default state must be last
- Layer list: last item drawn on top
- Shape drawable: `<shape>` with `<corners>`, `<gradient>`, `<solid>`, `<stroke>`, `<padding>`, `<size>`
- Style = View attributes collection; Theme = style applied to Activity/App
- Inheritance: via parent attribute (platform styles) or dot notation (own styles)
- `colorPrimary` → app bar; `colorPrimaryDark` → status bar; `colorAccent` → highlights/FAB/switches

---
---

# CHAPTER 5.2: Material Design

## Concept Overview
**Material Design** is Google's visual design philosophy (introduced 2014) for a unified user experience across platforms and device sizes. Based on real-world material metaphors — elements cast shadows, occupy space, and interact with each other.

---

## Theory & Logic

### Three Principles of Material Design
1. **"Material" metaphor** — elements behave like real-world materials; cast shadows, occupy space
2. **Bold, graphic, intentional** — deliberate colors, edge-to-edge imagery, large typography, intentional white space
3. **Meaningful motion** — animations respond to user actions, don't happen at random; user is the primary mover

### Colors in Material Design

**Color palette structure:**
- Choose a "500" shade as your **primary color** (brand color)
- Choose a darker shade as **colorPrimaryDark**
- Choose a shade starting with "A" as the **accent color**

**Three key colors in themes:**
```xml
<resources>
    <color name="colorPrimary">#3F51B5</color>     <!-- Indigo; used for app bar -->
    <color name="colorPrimaryDark">#303F9F</color>  <!-- Darker indigo; used for status bar -->
    <color name="colorAccent">#FF4081</color>       <!-- Pink; used for switches, FAB, highlights -->
</resources>
```

**Where they appear:**
- `colorPrimary` → app bar background
- `colorPrimaryDark` → status bar background
- `colorAccent` → switches (ON state), FAB, selected text highlight

**Contrast principle:** Dark background → light text; light background → dark text. Material themes handle this automatically:
- `Theme.AppCompat` → dark background → near-white text
- `Theme.AppCompat.Light` → light background → near-black text
- `Theme.AppCompat.Light.DarkActionBar` → light app body, dark app bar → light action bar text

**Opacity for text:**
- Set opacity using `#ARGB` or `#AARRGGBB` format
- Alpha channel: `FF` = fully opaque; `00` = fully transparent
- Convert percentage: 87% opacity = 0.87 × 255 = 222 → hex = DE
- Example: `#deffffff` = 87% opaque white (for primary text on dark background)

### Typography in Material Design

**Roboto** is the standard Material Design typeface. Six weights: Thin, Light, Regular, Medium, Bold, Black.

**Using predefined text appearances:**
```xml
<!-- Use TextAppearance.AppCompat.Display3 style -->
<TextView
    android:textAppearance="@style/TextAppearance.AppCompat.Display3"
    android:text="Large Display Text" />
```

Predefined styles: Display4, Display3, Display2, Display1, Headline, Title, Subhead, Body2, Body1, Caption, Button, Menu.
Text sizes use `sp` (scaleable pixels) for accessibility.

### Layout Metrics and Keylines

**8dp grid:** All components align to an 8dp square grid.
- Status bar: 24dp tall
- App bar (toolbar): 56dp tall
- Screen margins: 16dp from edges

**4dp grid:** Iconography in toolbars aligns to 4dp grid.

**Keylines:** Outlines marking content placement boundaries.
- Left screen edge: 16dp
- Content associated with icon/avatar: 72dp
- Right screen edge: 16dp

**Baseline grid:** Typography aligns to 4dp horizontal baseline grid.

### Material Design Components (via Design Support Library)

**Add Design Support Library:**
```groovy
compile 'com.android.support:design:25.0.1'
```

**Floating Action Button (FAB):**
```xml
<android.support.design.widget.FloatingActionButton
    android:id="@+id/addNewItemFAB"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/ic_plus_sign"
    app:fabSize="normal"     <!-- normal=56dp, mini=40dp, auto=varies with window -->
    app:elevation="10%" />
```

**Navigation Drawer:**
```xml
<android.support.v4.widget.DrawerLayout
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Main content (shown when drawer is hidden) -->
    <FrameLayout
        android:id="@+id/content_frame"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

    <!-- Navigation drawer (240dp wide, slides from left) -->
    <ListView
        android:id="@+id/left_drawer"
        android:layout_width="240dp"
        android:layout_height="match_parent"
        android:layout_gravity="start"     <!-- 'start' = left in LTR, right in RTL -->
        android:choiceMode="singleChoice"
        android:background="#111" />
</android.support.v4.widget.DrawerLayout>
```

**Snackbar:**
```java
// Simple snackbar (associate with CoordinatorLayout for extra features)
Snackbar.make(
    findViewById(R.id.myCoordinatorLayout),   // root view
    R.string.email_sent,                       // message
    Snackbar.LENGTH_SHORT                      // duration: SHORT, LONG, INDEFINITE
).show();
```

**Snackbar + CoordinatorLayout features:**
- User can swipe to dismiss
- FAB moves up when snackbar appears (instead of overlapping)
- Snackbar vs. Toast: snackbar can be swiped away; toast cannot

**Cards (CardView):**
```groovy
compile 'com.android.support:cardview-v7:24.2.1'
```
```xml
<android.support.v7.widget.CardView
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:cardCornerRadius="4dp"
    app:cardElevation="2dp">
    <!-- Card content here -->
</android.support.v7.widget.CardView>
```

**Lists:** Use RecyclerView (covered in 4.4).
```groovy
compile 'com.android.support:recyclerview-v7:24.2.1'
```

### Material Design Motion (Animations)

**Three animation types:**
1. **Property Animation** (API 11+) — most flexible; changes object properties over time
2. **View Animation** — older; only for Views; simpler for basic cases
3. **Drawable Animation** — loads series of drawable resources one after another

**Touch feedback (ripple effect):**
```xml
<!-- Bounded ripple (stays within view) -->
android:background="?android:attr/selectableItemBackground"

<!-- Unbounded ripple (extends beyond view) -->
android:background="?android:attr/selectableItemBackgroundBorderless"
```

**Circular Reveal Animation:**
```java
// Reveal a previously invisible view
View myView = findViewById(R.id.my_view);
int cx = myView.getWidth() / 2;    // center X
int cy = myView.getHeight() / 2;   // center Y
float finalRadius = (float) Math.hypot(cx, cy);  // final radius = hypot of w/2 and h/2

// Create animator (starts at radius=0, ends at finalRadius)
Animator anim = ViewAnimationUtils.createCircularReveal(myView, cx, cy, 0, finalRadius);
myView.setVisibility(View.VISIBLE);
anim.start();

// Hide a view with circular reveal
final View myView = findViewById(R.id.my_view);
int cx = myView.getWidth() / 2;
int cy = myView.getHeight() / 2;
float initialRadius = (float) Math.hypot(cx, cy);

Animator anim = ViewAnimationUtils.createCircularReveal(myView, cx, cy, initialRadius, 0);
anim.addListener(new AnimatorListenerAdapter() {
    @Override
    public void onAnimationEnd(Animator animation) {
        super.onAnimationEnd(animation);
        myView.setVisibility(View.INVISIBLE);
    }
});
anim.start();
```

**Activity Transitions:**
```xml
<!-- In styles.xml -->
<style name="BaseAppTheme" parent="android:Theme.Material">
    <item name="android:windowActivityTransitions">true</item>
    <item name="android:windowEnterTransition">@transition/explode</item>
    <item name="android:windowExitTransition">@transition/explode</item>
    <item name="android:windowSharedElementEnterTransition">@transition/change_image_transform</item>
    <item name="android:windowSharedElementExitTransition">@transition/change_image_transform</item>
</style>
```

```java
// Start activity with transitions
startActivity(intent, ActivityOptions.makeSceneTransitionAnimation(this).toBundle());

// In code instead of XML:
getWindow().requestFeature(Window.FEATURE_CONTENT_TRANSITIONS);
getWindow().setExitTransition(new Explode());
```

**Transition types:**
- **Enter transition** — how views enter the scene (e.g., explode = fly in from outside)
- **Exit transition** — how views exit the scene
- **Shared element transition** — same view transitions between activities (e.g., `changeImageTransform`)

**Curved motion (PathInterpolator):**
```xml
<!-- Custom path interpolator in XML -->
<pathInterpolator xmlns:android="http://schemas.android.com/apk/res/android"
    android:controlX1="0.4"
    android:controlY1="0"
    android:controlX2="1"
    android:controlY2="1" />
```

System provides three standard curves:
- `@interpolator/fast_out_linear_in.xml`
- `@interpolator/fast_out_slow_in.xml`
- `@interpolator/linear_out_slow_in.xml`

---

## Common Exam Traps / Edge Cases
- `colorPrimary` → app bar (NOT status bar); `colorPrimaryDark` → status bar
- `colorAccent` → switches (ON), FAB, selected text — not the primary app color
- Opacity percentage to hex: multiply by 255, convert to hex
- Snackbar unlike Toast: can be swiped away; FAB moves up if in CoordinatorLayout
- Motion must be **responsive, natural, aware, intentional** — the 4 principles
- Shared element transitions require the elements to have the same transitionName
- CircularReveal: radius 0→finalRadius to reveal; initialRadius→0 to hide (set INVISIBLE in AnimatorListenerAdapter)

---

## Quick Revision Bullets
- 3 Material Design principles: material metaphor, bold/graphic/intentional, meaningful motion
- colorPrimary = app bar; colorPrimaryDark = status bar; colorAccent = highlights/FAB/switches
- 8dp grid for layout; 4dp grid for icons in toolbar; 4dp baseline grid for typography
- Design Support Library: FAB, Snackbar, Navigation Drawer, Tabs, CoordinatorLayout
- Snackbar > Toast: swipeable, works with CoordinatorLayout to avoid FAB overlap
- 3 animation types: Property animation (most flexible), View animation (older, Views only), Drawable animation
- Touch feedback: `?android:attr/selectableItemBackground` for bounded ripple
- Activity transitions: enter, exit, shared element — enable with `windowActivityTransitions`

---
---

# CHAPTER 5.3: Providing Resources for Adaptive Layouts

## Concept Overview
An **adaptive layout** works well across different screen sizes, orientations, locales, and Android versions. Achieved by **externalizing resources** and providing **alternative resources** for specific device configurations.

---

## Theory & Logic

### Why Externalize Resources?
- Maintain resources separately from code — change once, affects everywhere it's used
- Provide alternative resources for different configurations (languages, screen sizes)
- Required for localization (translation)

### Standard Resource Folder Names

| Folder | Resource Type |
|--------|--------------|
| `animator/` | Property animations (XML) |
| `anim/` | Tween animations (XML) |
| `color/` | Color state lists (different from colors.xml in values/) |
| `drawable/` | Bitmaps and drawable XML files |
| `mipmap/` | Launcher icons for different densities |
| `layout/` | UI layout XML files |
| `menu/` | Menu XML files |
| `raw/` | Arbitrary raw files (read with `Resources.openRawResource()`) |
| `values/` | strings.xml, colors.xml, dimens.xml, styles.xml, arrays.xml |
| `xml/` | Arbitrary XML files (searchable config, preferences) |

### Alternative Resources

**Naming convention:**
```
<resource_folder_name>-<config_qualifier>
```

**Examples:**
```
res/values/strings.xml              ← default (English)
res/values-ja/strings.xml           ← Japanese
res/values-v21/styles.xml           ← API 21+
res/drawable/icon.png               ← default
res/drawable-hdpi/icon.png          ← high density screens
res/layout-land/activity_main.xml   ← landscape orientation
res/layout-ldrtl-night/             ← right-to-left layout + night mode (multiple qualifiers)
```

**Multiple qualifiers:** separate with dash; must be listed in order from Table 2 (precedence order).

### Common Configuration Qualifiers (in precedence order)

| Qualifier | Values | Example |
|-----------|--------|---------|
| MCC/MNC | Mobile country/network code | `mcc310-mnc004` |
| Language + region | BCP 47 language tag | `en`, `ja`, `fr-rFR` |
| Layout direction | `ldltr`, `ldrtl` | `ldrtl` (right-to-left) |
| Smallest width | `swNdp` | `sw600dp` (tablet) |
| Available width | `wNdp` | `w820dp` |
| Available height | `hNdp` | `h500dp` |
| Screen size | `small`, `normal`, `large`, `xlarge` | `large` |
| Screen aspect | `long`, `notlong` | `long` |
| Round screen | `round`, `notround` | `round` (wear) |
| Screen orientation | `port`, `land` | `land` (landscape) |
| UI mode | `car`, `desk`, `television`, `appliance`, `watch`, `vrheadset` | `television` |
| Night mode | `night`, `notnight` | `night` |
| Screen pixel density | `ldpi`, `mdpi`, `hdpi`, `xhdpi`, `xxhdpi`, `xxxhdpi` | `xxhdpi` |
| Touchscreen type | `notouch`, `stylus`, `finger` | `finger` |
| Keyboard | `nokeys`, `qwerty`, `12key` | `qwerty` |
| Navigation | `nonav`, `dpad`, `trackball`, `wheel` | `dpad` |
| Platform version | `vN` | `v21`, `v16` |

### Providing Default Resources

Always provide default resources (no qualifier). If no alternative matches, Android uses the default.

```
res/
├── values/
│   ├── strings.xml     ← DEFAULT (must always exist)
│   └── dimens.xml      ← DEFAULT
├── values-ja/
│   └── strings.xml     ← Japanese override
├── values-v21/
│   └── styles.xml      ← API 21+ override
├── drawable/
│   └── icon.png        ← DEFAULT
├── drawable-hdpi/
│   └── icon.png        ← hdpi screens
└── layout/
    ├── activity_main.xml     ← DEFAULT
    └── activity_main.xml (w820dp)  ← wide screens (shown in Android view as qualifier)
```

**Selection process:** Android matches the current device's configuration against available qualifiers. More specific qualifiers take precedence.

---

## Common Exam Traps / Edge Cases
- When using multiple qualifiers, they must be listed in **precedence order** (as in Table 2) — wrong order = folder ignored
- `color/` folder = color state lists (different from `colors.xml` in `values/`)
- `raw/` files are NOT given a resource ID; access via `Resources.openRawResource(R.raw.filename)`
- `assets/` folder = files NOT given resource IDs; read with `AssetManager` — different from `res/raw/`
- Default resources are MANDATORY — if device configuration doesn't match any alternative, Android uses default

---

## Quick Revision Bullets
- Alternative resources: `<folder_name>-<qualifier>` naming convention
- Multiple qualifiers: separate with dash; must be in precedence order
- Default resources are required; alternatives are optional overrides
- Standard folders: drawable, layout, menu, mipmap, values, animator, anim, color, raw, xml
- Language qualifier: e.g., `values-ja/` for Japanese; `drawable-hdpi/` for high-density
- Orientation qualifier: `land` for landscape; `port` for portrait
- Platform version qualifier: `v21` means API 21 and above
- Adaptive layout = right resources served to the right device configuration automatically

---
---

# CHAPTER 6.1: Testing the User Interface (Espresso + UI Automator)

## Concept Overview
**Espresso** is the framework for UI testing within a single app. **UI Automator** tests interactions between apps (including system apps). Both are part of the Android Testing Support Library and run as **instrumented tests**.

---

## Theory & Logic

### Espresso Basics

Espresso tests run on the device/emulator. Three main API components:

| Component | Method | Purpose |
|-----------|--------|---------|
| `onView(matcher)` | `ViewMatchers` | Find a view by its properties |
| `.perform(action)` | `ViewActions` | Perform an action on the view |
| `.check(assertion)` | `ViewAssertions` | Check view's state |

**Espresso test structure:**
```java
onView(withId(R.id.my_view))        // find the view
    .perform(click())               // perform an action
    .check(matches(isDisplayed())); // check the result
```

### Setting Up Espresso

**In build.gradle:**
```groovy
android {
    defaultConfig {
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
}

dependencies {
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    androidTestCompile 'com.android.support.test:runner:0.5'
    androidTestCompile 'com.android.support.test:rules:0.5'
}
```

### Writing Espresso Tests

```java
@RunWith(AndroidJUnit4.class)       // Espresso requires AndroidJUnit4
public class MainActivityTest {

    // ActivityTestRule launches the activity before each test
    @Rule
    public ActivityTestRule<MainActivity> mActivityRule =
            new ActivityTestRule<>(MainActivity.class);

    @Test
    public void testClickButton() {
        // Find view by ID, perform click
        onView(withId(R.id.my_button)).perform(click());

        // Check that a TextView now displays expected text
        onView(withId(R.id.my_textview))
                .check(matches(withText("Clicked!")));
    }

    @Test
    public void testTypeInEditText() {
        // Type text into an EditText
        onView(withId(R.id.editText_main))
                .perform(typeText("Hello"));

        // Close keyboard then check value
        onView(withId(R.id.editText_main))
                .perform(closeSoftKeyboard())
                .check(matches(withText("Hello")));
    }
}
```

### ViewMatchers (Finding Views)

```java
withId(R.id.my_view)               // by resource ID (most reliable)
withText("Hello World")             // by text content
withContentDescription("Button")   // by accessibility description
isDisplayed()                       // only visible views
isEnabled()                         // only enabled views
isChecked()                         // only checked views
withClassName(is("android.widget.Button"))  // by class name
```

### ViewActions (Performing Actions)

```java
click()                            // single click
longClick()                        // long click
doubleClick()                      // double click
typeText("Hello")                  // type text (clears first)
replaceText("World")               // replace all text
clearText()                        // clear text field
closeSoftKeyboard()                // close keyboard
pressBack()                        // press back button
scrollTo()                         // scroll to view (in ScrollView)
swipeLeft(), swipeRight()          // swipe actions
swipeUp(), swipeDown()             // swipe actions
```

### ViewAssertions (Checking Results)

```java
matches(isDisplayed())             // view is visible
matches(withText("Hello"))        // view has this text
matches(isEnabled())               // view is enabled
matches(isChecked())               // view is checked
doesNotExist()                     // view doesn't exist in hierarchy
```

### Testing RecyclerView Items

RecyclerView requires special handling because items may not be on screen:
```java
// Click on item at position 2 in RecyclerView
onView(withId(R.id.recyclerview))
    .perform(RecyclerViewActions.actionOnItemAtPosition(2, click()));

// Check text of a specific item
onView(withRecyclerView(R.id.recyclerview).atPosition(14))
    .check(matches(withText("Word 14")));
```

### Recording Espresso Tests (Android Studio 2.2+)

1. Run > Record Espresso Test → select deployment target → OK
2. Use the app normally (click, scroll, etc.)
3. Click "Add Assertion" to verify state
4. Click "Complete Recording" → saves test code

### Setting Up UI Automator

```groovy
androidTestCompile 'com.android.support.test.uiautomator:uiautomator-v18:2.1.2'
```

UI Automator can span **multiple apps** and access the Android system. Tests run on API 18+.

### Writing UI Automator Tests

```java
@RunWith(AndroidJUnit4.class)
@SdkSuppress(minSdkVersion = 18)  // UI Automator requires API 18+
public class ChangeTextBehaviorTest {

    private static final String BASIC_SAMPLE_PACKAGE = "com.example.android.testing";
    private static final int LAUNCH_TIMEOUT = 5000;
    private UiDevice mDevice;

    @Before
    public void startMainActivityFromHomeScreen() {
        // Get UiDevice instance
        mDevice = UiDevice.getInstance(InstrumentationRegistry.getInstrumentation());

        // Start from home screen
        mDevice.pressHome();

        // Wait for launcher to appear
        final String launcherPackage = mDevice.getLauncherPackageName();
        assertThat(launcherPackage, notNullValue());
        mDevice.wait(Until.hasObject(By.pkg(launcherPackage).depth(0)), LAUNCH_TIMEOUT);

        // Launch the app
        Context context = InstrumentationRegistry.getContext();
        final Intent intent = context.getPackageManager()
                .getLaunchIntentForPackage(BASIC_SAMPLE_PACKAGE);
        intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TASK);
        context.startActivity(intent);

        // Wait for app to appear
        mDevice.wait(Until.hasObject(By.pkg(BASIC_SAMPLE_PACKAGE).depth(0)), LAUNCH_TIMEOUT);
    }

    @Test
    public void testClickOkButton() {
        // Find OK button by text and class
        UiObject okButton = mDevice.findObject(new UiSelector()
                .text("OK")
                .className("android.widget.Button"));

        // Perform action
        if (okButton.exists() && okButton.isEnabled()) {
            okButton.click();
        }

        // Verify result
        UiObject result = mDevice.findObject(By.res(BASIC_SAMPLE_PACKAGE, "result"));
        assertEquals("5", result.getText());
    }
}
```

### UI Automator Key Classes

| Class | Purpose |
|-------|---------|
| `UiDevice` | Represents the device; device-level actions (pressHome, rotate, etc.) |
| `UiObject` | Represents a UI element; perform actions or query properties |
| `UiSelector` | Defines criteria to find a UI element |
| `UiCollection` | Group of UI elements (e.g., a list) |
| `UiScrollable` | Scrollable container; use for off-screen elements |

### UiSelector Examples

```java
// Find by text
mDevice.findObject(new UiSelector().text("Cancel"))

// Find by class
mDevice.findObject(new UiSelector().className("android.widget.Button"))

// Find by resource ID (preferred — most stable)
mDevice.findObject(By.res(PACKAGE, "my_button"))

// Chaining selectors
mDevice.findObject(new UiSelector()
        .text("OK")
        .className("android.widget.Button"))

// Nested selector (child within parent)
UiObject appItem = new UiObject(new UiSelector()
        .className("android.widget.ListView")
        .instance(1)
        .childSelector(new UiSelector().text("List Item 14")));
```

### UiScrollable (Scrolling to Off-Screen Elements)

```java
// Scroll to find "About phone" in Settings
UiScrollable settingsItem = new UiScrollable(new UiSelector()
        .className("android.widget.ListView"));

UiObject about = settingsItem.getChildByText(new UiSelector()
        .className("android.widget.LinearLayout"), "About phone");
about.click();
```

### Making UI Elements Accessible for UI Automator

```xml
<!-- Add contentDescription for ImageButton, ImageView, CheckBox -->
<RadioButton
    android:id="@+id/sameday"
    android:text="@string/same_day"
    android:contentDescription="@string/same_day"    <!-- for UI Automator + accessibility -->
    android:onClick="onRadioButtonClicked" />

<!-- Add hint for EditText -->
<EditText
    android:hint="@string/enter_text"                <!-- UI Automator uses hint -->
    android:contentDescription="@string/enter_text" />
```

**Rules:**
- Always add `android:contentDescription` to image-based views
- Add `android:hint` to EditText fields (UI Automator looks for hint, not contentDescription)
- Prefer resource IDs in selectors over text (text-based selectors break with translation)

### Running Instrumented Tests

```
To run a single test: right-click test method → Run
To run all tests in a class: right-click test file → Run
To run all tests in a directory: right-click directory → Run tests
```

Results appear in the **Run window**.

---

## Common Exam Traps / Edge Cases
- Espresso = single-app testing; UI Automator = multi-app testing
- `@SdkSuppress(minSdkVersion = 18)` is REQUIRED for UI Automator tests
- `ActivityTestRule` launches AND tears down activity for each test
- RecyclerView needs `RecyclerViewActions.actionOnItemAtPosition()` — regular `onView().perform(click())` doesn't work for off-screen items
- UI Automator: prefer resource IDs over text in selectors (text changes with translation)
- Espresso tests run on device; local unit tests run on JVM — they're in DIFFERENT source sets
- `mDevice.pressHome()` at the start of UI Automator tests is best practice
- `findObject()` returns first matching element (left to right, top to bottom); if none found → UiAutomatorObjectNotFoundException

---

## Quick Revision Bullets
- Espresso = in-app UI testing; UI Automator = cross-app UI testing
- Espresso: `onView(matcher).perform(action).check(assertion)`
- Key ViewMatchers: `withId()`, `withText()`, `isDisplayed()`, `isEnabled()`
- Key ViewActions: `click()`, `typeText()`, `scrollTo()`, `swipeLeft()`
- Key ViewAssertions: `matches(isDisplayed())`, `matches(withText())`, `doesNotExist()`
- RecyclerView testing: use `RecyclerViewActions.actionOnItemAtPosition()`
- UI Automator: `UiDevice`, `UiObject`, `UiSelector`, `UiCollection`, `UiScrollable`
- Always `mDevice.pressHome()` then launch app at start of UI Automator tests
- Accessibility: add `contentDescription` to image views; `hint` to EditText fields
- `@SdkSuppress(minSdkVersion = 18)` required for UI Automator
