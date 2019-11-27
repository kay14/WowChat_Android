# WowChat SDK

The **WowChat SDK** has been built using the [Firebase Realtime Database](https://firebase.google.com/docs/database). It is an open source framework which lets you add chat functionality to your existing Android application. It is easy to integrate and provides you with a couple of basic chat functionalities out of the box along with the user interface. Some of the key features include:

- Viewing the chat list screen, which lists all your conversations
- Viewing the chat details screen, which lists all the messages shared between you and the other user of interest
- Supports 6 different types of messages
- Supports 5 types of media files in messages - image, audio, video, document & contact
- Supports the feature to star and unstar messages
- Allows user to record audio and send it to other user
- Allows user to forward messages to other users through the app
- Allows user to share message with other user using other 3rd party app such as WhatsApp, Facebook, etc.

----------

## Integration

### Adding the framework into your project:
- Open your project in Android Studio.
- Download the library `wowchat` (using Git, or a zip archive to unzip).
- Go to **File** → **New** → **Import Module** and specify the source directory to import the library as a module.
- Right-click your app in project view and select **Open Module Settings**.
- Click the **Dependencies** tab and then the **“+“** button and select **Module Dependency**.
- Select the module `wowchat` to be added as dependency and assign **“implementation“** as the scope to this new dependency.
- Click **OK** and complete the process. Your app should build again.

----------

## Usage

### Add Firebase to your project:
- **Create a Firebase Project:**
  - In the [Firebase console](https://console.firebase.google.com/), click **Add project**, then select or enter a **Project name**. If you have an existing Google Cloud Platform (GCP) project, you can select the project from the dropdown menu to add Firebase resources to that project.
  - Click **Continue**.
  - Click **Create project** (or **Add Firebase**, if you're using an existing GCP project).
  
- **Register your app with Firebase:**
  - Open your newly created Firebase project, and in the **Firebase console's project overview page**, click the **Android icon** to launch the setup workflow. If you've already added an app to your Firebase project, click **Add app** to display the platform options.
  - Enter your app's `package name` in the **Android package name** field.
  - Click **Register app**.
  
- **Add a Firebase configuration file:**
  - Click **Download google-services.json** to obtain your Firebase Android config file (`google-services.json`).
  - Move your config file into the module (app-level) directory of your app.
  - To enable Firebase products in your app, add the **google-services plugin** to your Gradle files.
  - In your root-level (project-level) Gradle file (`build.gradle`), add rules to include the Google Services plugin. Check that you have Google's Maven repository, as well.   
    ```java
      buildscript {
      
        repositories {
          // Check that you have the following line (if not, add it):
          google()  // Google's Maven repository
        }
        
        dependencies {
          // ...
          
          // Add the following line:
          classpath 'com.google.gms:google-services:4.3.3'  // Google Services plugin
        }
      }
      
      allprojects {
        // ...
        
        repositories {
          // Check that you have the following line (if not, add it):
          google()  // Google's Maven repository
          // ...
        }
      }
    ```
        
  - In your module (app-level) Gradle file (usually `app/build.gradle`), add a line to the bottom of the file.
    ```java
      apply plugin: 'com.android.application'
      
      android {
        // ...
      }
      
      // Add the following line to the bottom of the file:
      apply plugin: 'com.google.gms.google-services'  // Google Play services Gradle plugin
    ```

> **NOTE:** As the required Firebase frameworks are included inside the WowChat framework itself, you don't have to include the Firebase SDK's in your app and initialize them.
If you wish to read further about the Firebase SDK [click here](https://firebase.google.com/docs).
  
### Initialize Framework:
- In your `Application.java` class:
  - Import `com.wowlabz.chat.ChatSDK` and `com.wowlabz.chat.WowChatApplication`.
  - Extend it from the `WowChatApplication` class
  - Invoke the `initialize(Context iContext)` function inside `onCreate()` to initialize the framework.
  
  Sample Code:
  ```java
  import com.wowlabz.chat.ChatSDK;
  import com.wowlabz.chat.WowChatApplication;

  public class YourApplication extends WowChatApplication {
    @Override
    public void onCreate() {
        super.onCreate();
        ChatSDK.getInstance().initialize(this).setDebugEnabled(true);
    }
  }  
  ```

### Set user:
- In your `Activity` class, set the user object before presenting the conversation list or detail screen.

  Sample Code:
  ```java
  User aUser = new User();
  aUser.setUid("9876543210");
  aUser.setName("John Doe");
  aUser.setImage("https://res.cloudinary.com/your_profile_image.jpg");
  ChatSDK.getInstance().setUser(aUser);
  ```

### Present the conversation list screen:
- In your `Activity` class, you can present the conversation list screen (after you have set the user object) to view the list of conversation you have had with other users.
  
  Sample Code:
  ```java
  ChatSDK.getInstance().presentInbox();
  ```

### Present the conversation detail screen:
- In your `Activity` class, you can present the conversation detail screen (after you have set user object) to directly initiate chat with another user.
  
  Sample Code:
  ```java
  ChatSDK.getInstance().chatWithUser("9876543211", new OnCompletionListener() {
                    @Override
                    public void onCompleted(Error iError) {
                        if(iError != null) {
                            // Show error
                        }
                    }
                });
  ```
 
----------

## Public methods in the Framework:



----------

> For usage, checkout our sample app [samplechatandroid]() on **Github**
