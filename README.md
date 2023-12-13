# w3a_spm_issue_demo

A Flutter project to showcase an error caused by using
[`cloud_firestore`](https://pub.dev/packages/cloud_firestore) and
[`single_factor_auth_flutter`](https://pub.dev/packages/single_factor_auth_flutter)
**simultaneously**.

## Issue

In iOS, `single_factor_auth_flutter` depends on **OpenSSL** whereas
`cloud_firestore` depends on **BoringSSL**
([BoringSSL](https://firebaseopensource.com/projects/firebase/boringssl/) is a
fork of OpenSSL that is designed to meet Google's needs).

When using both the packages simultaneously, BoringSSL is tampering with OpenSSL
files, which is manipulating it's header files.

As a result we are getting the following error while running for iOS:

```
Launching lib/main.dart on iPhone 14 Pro Max – iOS 16.4 in debug mode...
Running Xcode build...
Xcode build done.                                            7.1s
Failed to build iOS app
Lexical or Preprocessor Issue (Xcode): 'openssl_grpc/base.h' file not found
/Users/cumulations/Desktop/flutter_apps/w3a_spm_issue_demo/ios/Pods/BoringSSL-GRPC/src/include/openssl/aes.h:51:9

Could not build the application for the simulator.
Error launching application on iPhone 14 Pro Max – iOS 16.4.
```

**NOTE**: It is building just fine on Android.
