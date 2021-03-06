## Crash when selecting more than maxImages

This is a known bug with Matisse library, until it is fixed there you can fix it for you by adding the strings tranlastions as described [here](https://sh1d0w.github.io/multi_image_picker/#/theming?id=android-customization) .

## Android Support Version Mismatch

?> This error should no longer be present in version 3 of the plugin, as I've migrated it from the deprecated Android Support Library to AndroidX. If you are using multi_image_picker 3.* do not do this.

If you get errors like this:

!> Android dependency 'com.android.support:support-v4' has different version for the compile (X.X.X) and runtime (X.X.X) classpath.

This just means that your project uses several plugins that depend on different version of the support library. The suggested approach here is
to make all of them resolve to the same version, usually the highest one. To do so, in your `android/app/build.grade` go to `dependencies` and
add this:

```gradle
configurations.all {
  resolutionStrategy.eachDependency { DependencyResolveDetails details ->
    if (details.requested.group == 'com.android.support') {
      details.useVersion "27.1.1"
    }
  }
}
```

?> Don't forget to replace 27.1.1 with the highest version that the error you are getting is suggesting.

If you are getting error like this:

!> MultiImagePickerPlugin.java: 283 : error: cannot find symbol ExifInterface.TAG_ISO_SPEED

This also means you have version mismatch and should use the above solution, pinning the version to at least `27.1.1`
