# Android Library Integration Guide

## **1. Add Maven Repository to Project-level `build.gradle`**  
   Add the following code to your project-level `build.gradle` file:
```
buildscript {
    repositories {
        // Add the LmsWebView Maven repository
        maven {
            url "https://raw.githubusercontent.com/CircleLMS/android-library-sdk/refs/heads/main/"
            credentials {
                username = "username"
                password = "password"
            }
            authentication {
                basic(BasicAuthentication)
            }
        }
    }
}

allprojects {
    repositories {
        // Add the LmsWebView Maven repository
        maven {
            url "https://raw.githubusercontent.com/CircleLMS/android-library-sdk/refs/heads/main/"
            credentials {
                username = "username"
                password = "password"
            }
            authentication {
                basic(BasicAuthentication)
            }
        }
    }
}
```
🔐 Note: Use your GitHub username and password (or personal access token) for authentication.

## **2. Add Dependency to Module-level `build.gradle`** (version number varies)  
   In your **app/module-level** `build.gradle`, add the following inside the `dependencies` block:
```
dependencies {
    implementation 'com.accentrix.webview.library:LmsWebView:1.0.6'
}
```

## **3. Sync Gradle**  
   Sync your project with Gradle to resolve and download the AAR dependency.  
   
## **4. Import the Library in Your Code**  
   In the Java/Kotlin file where you want to use the WebView utility, import the following:  
```
   import com.accentrix.webview.library.util.WebViewUtil
```

## **5. Sample URLs:**  
Course catalog page: https://qasafetytraining.hercrentals.com/course/catalog  
Course detail page(used in email invitation): https://qasafetytraining.hercrentals.com/course/catalog/b8ba1023e33a11eab2fb0242ac120002  
My Training page: https://qasafetytraining.hercrentals.com/profile/assigned  

## **6. Sample Code:**  
```
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        val btLoadPage = findViewById<AppCompatButton>(R.id.btLoadPage)

        btLoadPage.setOnClickListener {
            LmsLaunchBuilder()
                .create(context = this, baseUrl = "https://safetytraining.hercrentals.com")
                .token(token = "access_token_here")
                .profile(LmsUserProfile(
                    accountNumber = "123456",
                    accountName = "John Doe",
                    role = "Admin",
                    driverLicense = "D12345678",
                    country = "US",
                    userType = "Credit",
                    phoneNumber = "+11234567890",
                    accountStatus = "A",
                    licenseState = "licenseState"))
                .launch()
        }
    }

}

```
