## Cracking the Android Encryption Challenge

This repository contains the solution to an Android encryption challenge, where a flag is hidden behind a username and password combination. The challenge utilizes AES encryption and requires careful analysis of the provided code to uncover the decryption key.

### Understanding the Challenge

**Encryption Method:** The app utilizes AES (Advanced Encryption Standard) encryption, a widely used symmetric encryption algorithm.

**Key Generation:** The decryption key appears to be derived from the username stored in the device's shared preferences and a predefined constant string. This approach creates a unique key for each user.

**IV (Initialization Vector):**  A constant IV is used in the encryption process. While convenient for demonstration purposes, a random IV should be used in real-world scenarios for better security.

### Solution Approach

1. **Code Analysis:** Examine the `MainActivity.java` file to understand the encryption logic, key generation, and output conditions.

2. **Username Analysis:** Identify the role of the username in the decryption process. The hint suggests that the username is part of the key.

3. **IV Identification:** Confirm the use of the predefined IV in the decryption process.

4. **Key Construction:** Concatenate the username with a predefined constant string to form the decryption key.

### Steps to Solve

1. **Retrieve the Username:** Obtain the username from the app's shared preferences.

2. **Construct the Key:** Combine the username with the predefined constant to form the decryption key.

3. **Decrypt the Flag:** Use the constructed key and the predefined IV to decrypt the encrypted flag using the AES algorithm in CBC mode.

**Code Implementation (Java):**

```java
// ... (code from MainActivity.java)

// Retrieve the username
String username = preferences.getString(ContantsKt.PREF_USERNAME, "");

// Construct the key
String decryptionKey = username + "111111111111";

// Decrypt the flag using AesEncryption (assuming you have implemented it)
String flag = AesEncryption.INSTANCE.decrypt(
    "mhVTa4HLNQRuxNNF/+/JJYUNyPvE4JsPe7h9ERBsSgjGxjq6nVtggZMMNXYrjCN0",
    new SecretKeySpec(decryptionKey.getBytes(StandardCharsets.UTF_8), "AES"),
    iv
);

// Log or display the decrypted flag
if (flag != null) {
    Log.i("Decrypted", flag);
    textMainActivity.setText("Flag: " + flag);
} else {
    Log.e("Decryption Error", "Failed to decrypt");
    textMainActivity.setText("Failed to decrypt. Please check your leet account.");
}
