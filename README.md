# oreo-shortcut

Android 8 Oreo (API 26) does *NOT* support an old BROADCAST way to create a pinned shortcut on home screen.

```java
// before Android 7.1
Intent intent = new Intent("com.android.launcher.action.INSTALL_SHORTCUT");
...
sendBroadcast(intent);
```

New Android 8 supports a new API way to create one.

`ShortcutManager#requestPinShortcut()`

```kotlin
// after Android 8.0
val manager = getSystemService(Context.SHORTCUT_SERVICE) as ShortcutManager
val info = ShortcutInfo.Builder(this, "shortcut-id")
    .setShortLabel("label") // must
    .setIntent(intent) // must
    .build()
manager.requestPinShortcut(info, null)
```

