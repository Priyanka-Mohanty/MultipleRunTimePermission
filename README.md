# Multiple Run Time Permission

Beginning in Android 6.0 (API level 23), users grant permissions to apps while the app is running, not when they install the app. This approach streamlines the app install process, since the user does not need to grant permissions when they install or update the app. It also gives the user more control over the app's functionality; for example, a user could choose to give a camera app access to the camera but not to the device location. The user can revoke the permissions at any time, by going to the app's Settings screen.

System permissions are divided into two categories, normal and dangerous:

Normal permissions do not directly risk the user's privacy. If your app lists a normal permission in its manifest, the system grants the permission automatically.
Dangerous permissions can give the app access to the user's confidential data. If your app lists a normal permission in its manifest, the system grants the permission automatically. If you list a dangerous permission, the user has to explicitly give approval to your app.

On all versions of Android, your app needs to declare both the normal and the dangerous permissions it needs in its app manifest, as described in Declaring Permissions. However, the effect of that declaration is different depending on the system version and your app's target SDK level:

If the device is running Android 5.1 or lower, or your app's target SDK is 22 or lower: If you list a dangerous permission in your manifest, the user has to grant the permission when they install the app; if they do not grant the permission, the system does not install the app at all.
If the device is running Android 6.0 or higher, and your app's target SDK is 23 or higher: The app has to list the permissions in the manifest, and it must request each dangerous permission it needs while the app is running. The user can grant or deny each permission, and the app can continue to run with limited capabilities even if the user denies a permission request.
## Note: Beginning with Android 6.0 (API level 23), users can revoke permissions from any app at any time, even if the app targets a lower API level. You should test your app to verify that it behaves properly when it's missing a needed permission, regardless of what API level your app targets

**First,Storing All the permissions in string Array:**
    
    `String[] permissions = new String[]{
            Manifest.permission.WRITE_EXTERNAL_STORAGE,
            Manifest.permission.CAMERA,
            Manifest.permission.ACCESS_COARSE_LOCATION,
            Manifest.permission.ACCESS_FINE_LOCATION,
            Manifest.permission.CALL_PHONE,
            Manifest.permission.SEND_SMS,
            Manifest.permission.ACCESS_NETWORK_STATE,
            Manifest.permission.INTERNET};`

**Check For All Permissions at a time**

    `public static final int REQUEST_ID_MULTIPLE_PERMISSIONS = 1;

     int result;
     List<String> listPermissionsNeeded = new ArrayList<>();
     for (String p : permissions) {
     result = ContextCompat.checkSelfPermission(getApplicationContext(), p);
     if (result != PackageManager.PERMISSION_GRANTED) {
     listPermissionsNeeded.add(p);
     }
     }
    if (!listPermissionsNeeded.isEmpty()) {
    ActivityCompat.requestPermissions(this,listPermissionsNeeded.toArray(new String[listPermissionsNeeded.size()]),    REQUEST_ID_MULTIPLE_PERMISSIONS);
    return false;
    }`

In this code, I am calling a method i.e **checkPermissions()** in MainActivity,where i am writing the code for accessing all the permission 

    `private boolean checkPermissions() {
        int result;
        List<String> listPermissionsNeeded = new ArrayList<>();
        for (String p : permissions) {
            result = ContextCompat.checkSelfPermission(getApplicationContext(), p);
            if (result != PackageManager.PERMISSION_GRANTED) {
                listPermissionsNeeded.add(p);
            }
        }
        if (!listPermissionsNeeded.isEmpty()) {
            ActivityCompat.requestPermissions(this, listPermissionsNeeded.toArray(new String[listPermissionsNeeded.size()]), REQUEST_ID_MULTIPLE_PERMISSIONS);
            return false;
        }
        return true;
    }`



# Output:
![First Screen](https://raw.githubusercontent.com/Priyanka-Mohanty/MultipleRunTimePermission/gh-pages/Images/Screenshot_20160803-120827.png)
![Second Screen](https://raw.githubusercontent.com/Priyanka-Mohanty/MultipleRunTimePermission/gh-pages/Images/Screenshot_20160803-120832.png)
![Third Screen](https://raw.githubusercontent.com/Priyanka-Mohanty/MultipleRunTimePermission/gh-pages/Images/Screenshot_20160803-120841.png)
![Fourth Screen](https://raw.githubusercontent.com/Priyanka-Mohanty/MultipleRunTimePermission/gh-pages/Images/Screenshot_20160803-120845.png)
![Fifth Screen](https://raw.githubusercontent.com/Priyanka-Mohanty/MultipleRunTimePermission/gh-pages/Images/Screenshot_20160803-120848.png)
![Sixth Screen](https://raw.githubusercontent.com/Priyanka-Mohanty/MultipleRunTimePermission/gh-pages/Images/Screenshot_20160803-120854.png)


