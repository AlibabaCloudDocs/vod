# How can I obtain a security file?

For security reasons, ApsaraVideo VOD encrypts videos and uses ApsaraVideo Player to decrypt the videos before they are played. In this case, a process of encryption and decryption is required. Before you use ApsaraVideo Player to download videos, you must obtain a security file. This topic describes how to obtain a security file.

## Intended audience

The developers who require a **security file** to download videos in ApsaraVideo Player.

## Enable secure download and generate a security file

1.  Activate ApsaraVideo VOD. For more information, see [Get started with ApsaraVideo VOD](/intl.en-US/Quick Start/Get started with ApsaraVideo VOD.md).
2.  Enable secure download in the ApsaraVideo VOD console. For more information, see [Configure offline download](/intl.en-US/User Guide/Domain management/Configure offline download.md).
3.  Obtain the unique application identifier.
    -   For Android users: Obtain a SHA-1 key.You can use the following sample code to generate the key:

        ```
        // Generate a SHA-1 key.
        public static String getCertificateSHA1Fingerprint(Context context) {
          // Obtain a package manager.
          PackageManager pm = context.getPackageManager();
          // Obtain the package name of the SHA-1 key. You can also use another package name.
          // However, if you use another package name, make sure that the context parameter that is passed specifies the context of the package.
          String packageName = context.getPackageName();
          // Return the signature that is included in the package.
          int flags = PackageManager.GET_SIGNATURES;
          PackageInfo packageInfo = null;
          try {
              // Obtain all content information of the package.
              packageInfo = pm.getPackageInfo(packageName, flags);
          }catch (PackageManager.NameNotFoundException e) {
              e.printStackTrace();
          }
          // The signature.
          Signature[] signatures = packageInfo.signatures;
          byte[] cert = signatures[0].toByteArray();
          // Convert the signature to a byte array stream.
          InputStream input = new ByteArrayInputStream(cert);
          // The certificate factory class, which implements the factory certificate algorithm.
          CertificateFactory cf = null;
          try {
              cf = CertificateFactory.getInstance("X509");
          } catch (CertificateException e) {
              e.printStackTrace();
          }
          // The X.509 certificate, which is a common certificate format.
          X509Certificate c = null;
          try {
              c = (X509Certificate) cf.generateCertificate(input);
          }catch (CertificateException e) {
              e.printStackTrace();
          }
          String hexString = null;
          try {
              // The encryption algorithm class. The parameter values can be encrypted by using the MD4 or MD5 algorithm.
              MessageDigest md = MessageDigest.getInstance("SHA1");
              // Obtain the public key.
              byte[] publicKey = md.digest(c.getEncoded());
              // Convert bytes to hexadecimal values.
              hexString = byte2HexFormatted(publicKey);
          }catch (NoSuchAlgorithmException e1) {
              e1.printStackTrace();
          }catch (CertificateEncodingException e) {
              e.printStackTrace();
          }
          return hexString;
        }
        // Convert the obtained code to a hexadecimal value.
        private static String byte2HexFormatted(byte[] arr){
          StringBuilder str = new StringBuilder(arr.length * 2);
          for (int i = 0; i < arr.length; i++) 
        {
              String h = Integer.toHexString(arr[i]);
              int l = h.length();
              if (l == 1)
                  h = "0" + h;
              if (l > 2)
                  h = h.substring(l - 2, l);
              str.append(h.toUpperCase());
              if (i < (arr.length - 1))
                  str.append(':');
          }
          return str.toString();}
        ```

    -   For iOS users: Enter the bundle ID.
    -   For Windows users: Call the serial number in the digital signature certificate of the .exe file in the SDK, as shown in the following figure.

        ![appId.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0415669161/p179097.png)

4.  Specify the private key for offline decryption. The value is a string of 16 to 32 characters in length and contains uppercase letters, lowercase letters, and digits.
5.  After you specify the parameters, click **Generate and Download Key**. The security file is generated.

**Note:** Before the algorithm for obtaining the SHA-1 key is provided, you must obtain the SHA-1 key of the signature of the default keystore. If you release a package of another keystore, we recommend that you configure the release keystore in the gradle file and obtain the SHA-1 key by using the preceding method.

Sample code of configuring a keystore:

```
// Use the following sample code to configure a keystore. You can replace the keystore file as needed. Before you configure the keystore, you must place the keystore file in the root directory of the project.
    signingConfigs {
        debug {
            storeFile file("$rootDir/debug.keystore")
            storePassword "android"
            keyAlias "androiddebugkey"
            keyPassword "android"
        }
        release {
            storeFile file("$rootDir/debug.keystore")
            storePassword "android"
            keyAlias "androiddebugkey"
            keyPassword "android"
        }
    }
        buildTypes {
        debug {
            multiDexEnabled true
            signingConfig signingConfigs.debug
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
        release {
            minifyEnabled true
            multiDexEnabled true
            signingConfig signingConfigs.release
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
```

