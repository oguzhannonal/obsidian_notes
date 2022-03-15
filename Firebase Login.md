**User Authentication** can be seen in every application nowadays. So Authentication is important for everyone, who is learning Flutter, to know.

In this article, I will be discussing how you can log in and register in Flutter.

We will be using the Firebase console for this. I will be discussing how you can authenticate in flutter using Email only.

Don’t worry I will be discussing log in using **Google** and **Facebook** in future articles.

### Table of Contents:

1.  [Creating a Project in Firebase Console](https://kickertech.com/login-and-register-easily-with-flutter-using-firebase/#Creating-a-Project-in-Firebase-Console)
2.  [Designing a Simple UI for the app](https://kickertech.com/login-and-register-easily-with-flutter-using-firebase/#Designing-a-Simple-UI-for-the-app)
3.  [Adding the packages to Pubsec.yaml](https://kickertech.com/login-and-register-easily-with-flutter-using-firebase/#Adding-the-packages-to-Pubsec.yaml)
4.  [How to register in Flutter using email and password](https://kickertech.com/login-and-register-easily-with-flutter-using-firebase/#How-to-register-in-Flutter-using-email-and-password)
5.  [How to login in Flutter using email and password](https://kickertech.com/login-and-register-easily-with-flutter-using-firebase/#Login-using-Email-and-Password)
6.  [How to sign out of the application](https://kickertech.com/login-and-register-easily-with-flutter-using-firebase/#Signing-out-of-the-app)

**Now Let’s get started.**

## Flutter Login and Registration using Firebase

### First Step: Creating a Project in Firebase Console

We will be **creating/adding** a New Project in Firebase Console. If you don’t have an account, you can create one easily.

Write the Project Name and click **Continue**

![](https://kickertech.com/wp-content/uploads/2021/07/1-1.png?ezimgfmt=rs:740x518/rscb18/ng:webp/ngcb18)

We won’t be needing **Google Analytics** for this test. **Disable** Google Analytics, and click on **Create Project**

![](https://kickertech.com/wp-content/uploads/2021/07/2-1.png?ezimgfmt=rs:740x500/rscb18/ng:webp/ngcb18)

The Project is now created. Click on **Continue**

![](https://kickertech.com/wp-content/uploads/2021/07/4-1-1024x441.png?ezimgfmt=rs:740x318/rscb18/ng:webp/ngcb18)

Go to the **Project Overview** and Click on the **android** or **iOS** icon to continue.

![](https://kickertech.com/wp-content/uploads/2021/07/5-1-1024x422.png?ezimgfmt=rs:740x305/rscb18/ng:webp/ngcb18)

After you click on the Android/IOS icon, you will see this page. You have to put the name of your Android/IOS Package which is your `applicationId`.

![](https://kickertech.com/wp-content/uploads/2021/07/6.png?ezimgfmt=rs:740x537/rscb18/ng:webp/ngcb18)

You can find the **name** on `android/app/build.gradle`

```
 defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.login_logout_app" //this is the name
        minSdkVersion 21
        targetSdkVersion 30
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
        multiDexEnabled true
    }
```

Now you can leave the SHA-1 field empty because in our case we will only be logging with **email** and **password**. But if you have to log in with google or Facebook, you need to put the SHA-1.

Here’s how you can find the **SHA-1 certificate**. Here’s the link to the StackFlow: [**Where do I get SHA-1 certificate fingerprint using flutter?**](https://stackoverflow.com/questions/62867733/where-do-i-get-sha-1-certificate-fingerprint-using-flutter-using-flutter-creat)

Now Click on the **Register app**.

![](https://kickertech.com/wp-content/uploads/2021/07/image-11.png?ezimgfmt=rs:740x403/rscb18/ng:webp/ngcb18)

You have to download the **google-services.json** file and put that file in the `android/app` folder

![](https://kickertech.com/wp-content/uploads/2021/07/image-12.png?ezimgfmt=rs:740x461/rscb18/ng:webp/ngcb18)

The next step will be putting all those lines of code exactly as it is in the specified location.

![](https://kickertech.com/wp-content/uploads/2021/07/image-13.png?ezimgfmt=rs:740x469/rscb18/ng:webp/ngcb18)

Now you are all done. Click on **Continue to console**.

![](https://kickertech.com/wp-content/uploads/2021/07/image-14.png?ezimgfmt=rs:740x554/rscb18/ng:webp/ngcb18)

Click on **Authentication** in the dashboard. You will then see this page.

![](https://kickertech.com/wp-content/uploads/2021/07/image-15-1024x311.png?ezimgfmt=rs:740x225/rscb18/ng:webp/ngcb18)

Enable the **Email/Password** and Click on **Save**.

![](https://kickertech.com/wp-content/uploads/2021/07/image-16.png?ezimgfmt=rs:740x217/rscb18/ng:webp/ngcb18)

### Second Step: Designing a Simple UI for the app

We will be creating a simple UI for the user to Log in, Sign up, and HomeScreen.

![](https://kickertech.com/wp-content/uploads/2021/07/image-9.png?ezimgfmt=rs:279x496/rscb18/ng:webp/ngcb18)

**Login\_Screen** where user can log in with Email and Password

![](https://kickertech.com/wp-content/uploads/2021/07/image-8.png?ezimgfmt=rs:287x506/rscb18/ng:webp/ngcb18)

**Register\_Screen** to register the user using email and password

![](https://kickertech.com/wp-content/uploads/2021/07/homescreen.png?ezimgfmt=rs:295x525/rscb18/ng:webp/ngcb18)

**Home\_Screen** which the user sees after successfully logging in with email and password

### Third Step: Adding the packages to Pubsec.yaml

Adding the following Packages to `pubsec.yaml`

```
  firebase_auth: ^3.0.1
  firebase_core: ^1.4.0
```

### Fourth Step: Register using email and password

**Register\_Screen.dart**

Here are important fragments of codes from `Register_Screen`. You can find the full code on Github.

```
      //1
import 'package:firebase_auth/firebase_auth.dart';
      //2
  final _auth = FirebaseAuth.instance;
  String email = '';
  String password = '';
      //3
                            TextFormField(
                              keyboardType: TextInputType.emailAddress,
                              onChanged: (value) {
                                email = value.toString().trim();
                              },
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                hintText: 'Enter Your Email',
                                prefixIcon: Icon(
                                  Icons.email,
                                  color: Colors.black,
                                ),
                              ),
                            ),
              //4
                            TextFormField(
                              obscureText: true,
                              validator: (value) {
                                if (value!.isEmpty) {
                                  return "Please enter Password";
                                }
                              },
                              onChanged: (value) {
                                password = value;
                              },
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                  hintText: 'Choose a Password',
                                  prefixIcon: Icon(
                                    Icons.lock,
                                    color: Colors.black,
                                  )),
                            ),
           //5
                            LoginSignupButton(
                              title: 'Register',
                              ontapp: () async {
            (i)           
                                  try {
                                    await _auth.createUserWithEmailAndPassword(
                                        email: email, password: password);
                                    ScaffoldMessenger.of(context).showSnackBar(
                                      SnackBar(
                                          child: Text(
                                              'Sucessfully Register.You Can Login Now'),
                                        ),
                                        duration: Duration(seconds: 5),
                                      ),
                                    );
                                    Navigator.of(context).pop();
                  (ii)
                                  } on FirebaseAuthException catch (e) {
                                    showDialog(
                                      context: context,
                                      builder: (ctx) => AlertDialog(
                                        title:
                                            Text(' Ops! Registration Failed'),
                                        content: Text('${e.message}'),
                                      ......

```

First (1), we will be importing the **Firebase Authentication package** to our **Register\_Screen**.

After that (2), we will be creating an instance of **FirebaseAuth** and assign its value to **\_auth** which is used as Global value. We will be also declaring email and password as **String** and they will have **empty values**.

(3) is for the User to enter the email. ![](https://kickertech.com/wp-content/uploads/2021/07/7.png?ezimgfmt=rs:300x75/rscb18/ng:webp/ngcb18)

(4) is for the User to enter the password. ![](https://kickertech.com/wp-content/uploads/2021/07/8.png?ezimgfmt=rs:300x66/rscb18/ng:webp/ngcb18)

The entered value(email) is stored in the **email** String and the value(password) is stored in the **password** String.

At (5) where we have made **Register** Button. (i) The main work is to register the user after he has entered the email and password.

**Register** button calls for the method: `createUserWithEmailAndPassword()`. This method stores our email and password in the firebase console.

After registering, we will be directed to the **Login\_Screen**. The **snack bar** is shown to the user at the bottom with the message of successful registration.

The **credentials** are stored in Firebase with the `createUserWithEmailAndPassword()` method which is accessed from **\_auth**.

![](https://kickertech.com/wp-content/uploads/2021/07/image-19-1024x458.png?ezimgfmt=rs:740x331/rscb18/ng:webp/ngcb18)

(ii) If any error occurs, the error/exception is caught in the catch block, and the Dialog box is shown informing the user of the error.

![](https://kickertech.com/wp-content/uploads/2021/07/11.png?ezimgfmt=rs:294x518/rscb18/ng:webp/ngcb18)

### Fifth Step: Login using Email and Password

Here are important fragments of codes from `Login_Screen`. You can find the full code on Github.

The codes are similar to Register\_Screen codes.

These are the most important code that you should pay attention to.

**Login\_Screen.dart**

```
//1
import 'package:firebase_auth/firebase_auth.dart';
.....
//2
 final _auth = FirebaseAuth.instance;
  String email = '';
  String password = '';
.....
.....
//3
                            TextFormField(
                              keyboardType: TextInputType.emailAddress,
                              onChanged: (value) {
                                email = value;
                              },
                              },
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                hintText: 'Email',
                                prefixIcon: Icon(
                                  Icons.email,
                                  color: Colors.black,
                                ),
                              ),
                            ),
                            SizedBox(height: 30),
//4
                            TextFormField(
                              obscureText: true,
                              onChanged: (value) {
                                password = value;
                              },
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                  hintText: 'Password',
                                  prefixIcon: Icon(
                                    Icons.lock,
                                    color: Colors.black,
                                  )),
                            ),
                            SizedBox(height: 80),
//5
                            LoginSignupButton(
                              title: 'Login',
                              ontap: () async {
                                             try {
                                    await _auth.signInWithEmailAndPassword(
                                        email: email, password: password);
                                    await Navigator.of(context).push(
                                      MaterialPageRoute(
                                        builder: (contex) => HomeScreen(),
                                      ),
                                    );
                                                 } on FirebaseAuthException catch (e) {
                                    showDialog(
                                      context: context,
                                      builder: (ctx) => AlertDialog(
                                        title: Text("Ops! Login Failed"),
                                        content: Text('${e.message}'),
......

```

First (1), we will be importing the **Firebase Authentication** package to our `**Login_Screen**`.

After that (2), we will be creating an **instance** of **FirebaseAuth** and assign its value to **\_auth** which is used as Global value. We will be also declaring email and password as **String** and they will have **empty** values.

(3) is for the User to enter the email. ![](https://kickertech.com/wp-content/uploads/2021/07/7.png?ezimgfmt=rs:300x75/rscb18/ng:webp/ngcb18)

(4) is for the User to enter the password. ![](https://kickertech.com/wp-content/uploads/2021/07/8.png?ezimgfmt=rs:300x66/rscb18/ng:webp/ngcb18)

The entered value(email) is stored in the **email** String and the value(password) is stored in the **password** String.

At (5) where we have made Login Button.

```
 LoginSignupButton(
                              title: 'Login',
                              ontap: () async {
                                        //i
                                             try {
                                    await _auth.signInWithEmailAndPassword(
                                        email: email, password: password);
                                    await Navigator.of(context).push(
                                      MaterialPageRoute(
                                        builder: (contex) => HomeScreen(),
                                      ),
                                    );
                                         //ii
                                                 } on FirebaseAuthException catch (e) {
                                    showDialog(
                                      context: context,
                                      builder: (ctx) => AlertDialog(
                                        title: Text("Ops! Login Failed"),
                                        content: Text('${e.message}'),
```

After the user has entered email and password, he will tap on the **Login** button.

Login button calls for the method: \_signInWithEmailAndPassword(). This method (i) is where we will pass the email and password to Firebase for authentication and retrieve the FirebaseUser object. This will match the email and password with the data stored in the firebase.

If the records are correct we will be directed to the **Home\_Screen**.

![](https://kickertech.com/wp-content/uploads/2021/07/homescreen.png?ezimgfmt=rs:268x477/rscb18/ng:webp/ngcb18)

If the records are incorrect, an exception will occur which will show a dialog box.

![](https://kickertech.com/wp-content/uploads/2021/07/9.png?ezimgfmt=rs:270x478/rscb18/ng:webp/ngcb18)

The authentication and showing exceptions are done inside the **try and catch** block as you can see in the code above.

### Sixth Step: Signing out of the app

**Home\_Screen**

The Home\_Screen has a very simple UI and there is only one button for **logout**.

![](https://kickertech.com/wp-content/uploads/2021/07/homescreen.png?ezimgfmt=rs:342x608/rscb18/ng:webp/ngcb18)

The implementation is simple as well. We first have to create the **instance** of Firebase and assign it to **\_firebaseAuth**.

We will then create a simple asynchronous method \_signOut() and access the signOut object from the instance `_firebaseAuth`.

Next, the signOut() method will be called when the user presses on the **Log out** button. The user is then logged out.

**Home\_Screen.dart**

```
import 'package:firebase_auth/firebase_auth.dart';
import 'package:flutter/material.dart';
import 'package:login_logout_app/Screens/Login_Screen.dart';
class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}
final FirebaseAuth _firebaseAuth = FirebaseAuth.instance;
_signOut() async {
  await _firebaseAuth.signOut();
}
class _HomeScreenState extends State<HomeScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.grey[200],
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('You have logged in Successfuly'),
            SizedBox(height: 50),
            Container(
              height: 60,
              width: 150,
              child: ElevatedButton(
                  clipBehavior: Clip.hardEdge,
                  child: Center(
                    child: Text('Log out'),
                  ),
                  onPressed: () async {
                    await _signOut();
                    if (_firebaseAuth.currentUser == null) {
                      Navigator.push(
                        context,
                        MaterialPageRoute(builder: (context) => LoginScreen()),
                      );
                    }
                  }),
            )
          ],
        ),
      ),
    );
  }
}

```

Now we are all done with authentication. Hope I was able to help you out and you were able to learn about register, log in, and log out in flutter.

**Here’s the Github link to this project: [Login\_Logout\_App](https://github.com/dragneel2074/login_logout_app)**

I will be writing about how you can log in using **Google** and **Facebook** in coming articles.

Thanks for reading.

**Register\_Screen Code**

```
import 'package:firebase_auth/firebase_auth.dart';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:login_logout_app/Component/button.dart';
import '../constants.dart';
import 'Login_Screen.dart';
class SignupScreen extends StatefulWidget {
  @override
  _SignupScreenState createState() => _SignupScreenState();
}
class _SignupScreenState extends State<SignupScreen> {
  final formkey = GlobalKey<FormState>();
  final _auth = FirebaseAuth.instance;
  String email = '';
  String password = '';
  bool isloading = false;
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.grey[200],
        elevation: 0,
        leading: IconButton(
          icon: Icon(Icons.arrow_back_ios, color: Colors.black,size: 30,),
          onPressed: () => Navigator.of(context).pop(),
        ),
      ),
      body: isloading
          ? Center(
              child: CircularProgressIndicator(),
            )
          : Form(
              key: formkey,
              child: AnnotatedRegion<SystemUiOverlayStyle>(
                value: SystemUiOverlayStyle.light,
                child: Stack(
                  children: [
                    Container(
                      height: double.infinity,
                      width: double.infinity,
                     color: Colors.grey[200],
                      child: SingleChildScrollView(
                        padding:
                            EdgeInsets.symmetric(horizontal: 25, vertical: 120),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.center,
                          children: [
                            Hero(
                              tag: '1',
                                                          child: Text(
                                "Sign up",
                                style: TextStyle(
                                    fontSize: 30,
                                    color: Colors.black,
                                    fontWeight: FontWeight.bold),
                              ),
                            ),
                            SizedBox(height: 30),
                            TextFormField(
                              keyboardType: TextInputType.emailAddress,
                              onChanged: (value) {
                                email = value.toString().trim();
                              },
                              validator: (value) => (value!.isEmpty)
                                  ? ' Please enter email'
                                  : null,
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                hintText: 'Enter Your Email',
                                prefixIcon: Icon(
                                  Icons.email,
                                  color: Colors.black,
                                ),
                              ),
                            ),
                            SizedBox(height: 30),
                            TextFormField(
                              obscureText: true,
                              validator: (value) {
                                if (value!.isEmpty) {
                                  return "Please enter Password";
                                }
                              },
                              onChanged: (value) {
                                password = value;
                              },
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                  hintText: 'Choose a Password',
                                  prefixIcon: Icon(
                                    Icons.lock,
                                    color: Colors.black,
                                  )),
                            ),
                            SizedBox(height: 80),
                            LoginSignupButton(
                              title: 'Register',
                              ontapp: () async {
                                if (formkey.currentState!.validate()) {
                                  setState(() {
                                    isloading = true;
                                  });
                                  try {
                                    await _auth.createUserWithEmailAndPassword(
                                        email: email, password: password);
                                    ScaffoldMessenger.of(context).showSnackBar(
                                      SnackBar(
                                        backgroundColor: Colors.blueGrey,
                                        content: Padding(
                                          padding: const EdgeInsets.all(8.0),
                                          child: Text(
                                              'Sucessfully Register.You Can Login Now'),
                                        ),
                                        duration: Duration(seconds: 5),
                                      ),
                                    );
                                    Navigator.of(context).pop();
                                    setState(() {
                                      isloading = false;
                                    });
                                  } on FirebaseAuthException catch (e) {
                                    showDialog(
                                      context: context,
                                      builder: (ctx) => AlertDialog(
                                        title:
                                            Text(' Ops! Registration Failed'),
                                        content: Text('${e.message}'),
                                        actions: [
                                          TextButton(
                                            onPressed: () {
                                              Navigator.of(ctx).pop();
                                            },
                                            child: Text('Okay'),
                                          )
                                        ],
                                      ),
                                    );
                                  }
                                  setState(() {
                                    isloading = false;
                                  });
                                }
                              },
                            ),
                          ],
                        ),
                      ),
                    )
                  ],
                ),
              ),
            ),
    );
  }
}

```

**Login\_Screen Codes**

```
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:firebase_auth/firebase_auth.dart';
import 'package:login_logout_app/Component/button.dart';
import '../constants.dart';
import 'Home_Screen.dart';
import 'Register_Screen.dart';
class LoginScreen extends StatefulWidget {
  @override
  _LoginScreenState createState() => _LoginScreenState();
}
class _LoginScreenState extends State<LoginScreen> {
  final formkey = GlobalKey<FormState>();
  final _auth = FirebaseAuth.instance;
  String email = '';
  String password = '';
  bool isloading = false;
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: isloading
          ? Center(
              child: CircularProgressIndicator(),
            )
          : Form(
              key: formkey,
              child: AnnotatedRegion<SystemUiOverlayStyle>(
                value: SystemUiOverlayStyle.light,
                child: Stack(
                  children: [
                    Container(
                      height: double.infinity,
                      width: double.infinity,
                      color: Colors.grey[200],
                      child: SingleChildScrollView(
                        padding:
                            EdgeInsets.symmetric(horizontal: 25, vertical: 120),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.center,
                          children: [
                            Text(
                              "Sign In",
                              style: TextStyle(
                                  fontSize: 50,
                                  color: Colors.black,
                                  fontWeight: FontWeight.bold),
                            ),
                            SizedBox(height: 30),
                            TextFormField(
                              keyboardType: TextInputType.emailAddress,
                              onChanged: (value) {
                                email = value;
                              },
                              validator: (value) {
                                if (value!.isEmpty) {
                                  return "Please enter Email";
                                }
                              },
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                hintText: 'Email',
                                prefixIcon: Icon(
                                  Icons.email,
                                  color: Colors.black,
                                ),
                              ),
                            ),
                            SizedBox(height: 30),
                            TextFormField(
                              obscureText: true,
                              validator: (value) {
                                if (value!.isEmpty) {
                                  return "Please enter Password";
                                }
                              },
                              onChanged: (value) {
                                password = value;
                              },
                              textAlign: TextAlign.center,
                              decoration: kTextFieldDecoration.copyWith(
                                  hintText: 'Password',
                                  prefixIcon: Icon(
                                    Icons.lock,
                                    color: Colors.black,
                                  )),
                            ),
                            SizedBox(height: 80),
                            LoginSignupButton(
                              title: 'Login',
                              ontapp: () async {
                                if (formkey.currentState!.validate()) {
                                  setState(() {
                                    isloading = true;
                                  });
                                  try {
                                    await _auth.signInWithEmailAndPassword(
                                        email: email, password: password);
                                    await Navigator.of(context).push(
                                      MaterialPageRoute(
                                        builder: (contex) => HomeScreen(),
                                      ),
                                    );
                                    setState(() {
                                      isloading = false;
                                    });
                                  } on FirebaseAuthException catch (e) {
                                    showDialog(
                                      context: context,
                                      builder: (ctx) => AlertDialog(
                                        title: Text("Ops! Login Failed"),
                                        content: Text('${e.message}'),
                                        actions: [
                                          TextButton(
                                            onPressed: () {
                                              Navigator.of(ctx).pop();
                                            },
                                            child: Text('Okay'),
                                          )
                                        ],
                                      ),
                                    );
                                    print(e);
                                  }
                                  setState(() {
                                    isloading = false;
                                  });
                                }
                              },
                            ),
                            SizedBox(height: 10),
                            GestureDetector(
                              onTap: () {
                                Navigator.of(context).push(
                                  MaterialPageRoute(
                                    builder: (context) => SignupScreen(),
                                  ),
                                );
                              },
                              child: Row(
                                children: [
                                  Text(
                                    "Don't have an Account ?",
                                    style: TextStyle(
                                        fontSize: 20, color: Colors.black87),
                                  ),
                                  SizedBox(width: 10),
                                  Hero(
                                    tag: '1',
                                    child: Text(
                                      'Sign up',
                                      style: TextStyle(
                                          fontSize: 21,
                                          fontWeight: FontWeight.bold,
                                          color: Colors.black),
                                    ),
                                  )
                                ],
                              ),
                            )
                          ],
                        ),
                      ),
                    )
                  ],
                ),
              ),
            ),
    );
  }
}

```

### Best Course for Learning Flutter:

(on Udemy)

[![](https://kickertech.com/wp-content/uploads/2022/02/Capture-1.png?ezimgfmt=rs:413x227/rscb18/ng:webp/ngcb18)](https://click.linksynergy.com/deeplink?id=w3WHd5KiuvA&mid=39197&u1=flutterlink&murl=https%3A%2F%2Fwww.udemy.com%2Fcourse%2Flearn-flutter-dart-to-build-ios-android-apps%2F)


[[Firebase]][[Bitirme Projesi]]