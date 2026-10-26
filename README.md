# Ex.No 2B: Factorial using Explicit Intent
 
## Aim
To create an Android application with two screens. The first screen takes a number from the user. After clicking the **Factorial** button, the second screen opens and displays the factorial of the same number using an **Explicit Intent**, developed in Android Studio.
 
## Equipment Required
- Latest version of Android Studio
- Android Emulator or a physical Android device
## Concept
An **Explicit Intent** names the exact component (Activity) to start, using the current context and the target class: `new Intent(MainActivity.this, SecondActivity.class)`. Data is passed between screens using `putExtra()` and read with `getIntExtra()`.
 
## Algorithm
1. Create a new Android Studio project (Empty Views Activity) named `ExplicitIntent`.
2. Design the first screen (`activity_main.xml`) with an `EditText` and a **Factorial** button.
3. In `MainActivity`, read the number on button click and validate it (not empty, between 0 and 20).
4. Create an explicit intent targeting `SecondActivity`, attach the number with `putExtra("number", num)`, and call `startActivity()`.
5. Design the second screen (`activity_second.xml`) with a `TextView` for the result and a **Go Back** button.
6. In `SecondActivity`, receive the number using `getIntExtra("number", 0)`.
7. Compute the factorial using a loop with a `long` variable (0! = 1).
8. Display the result as "Factorial of N is X".
9. On **Go Back**, call `finish()` to return to the first screen.
10. Register both activities in `AndroidManifest.xml`, then save and run.
## Project Details
| Item | Value |
|------|-------|
| App name | ExplicitIntent |
| Package | `com.example.explicitintent` |
| Language | Java |
| Min SDK | API 24 |
| Layout | ConstraintLayout |
 
## Program
 
### res/values/strings.xml
```xml
<resources>
    <string name="app_name">ExplicitIntent</string>
    <string name="title">Factorial Calculator</string>
    <string name="number_hint">Enter a number</string>
    <string name="factorial">Factorial</string>
    <string name="go_back">Go Back</string>
</resources>
```
 
### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
 
    <TextView
        android:id="@+id/txtTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="100dp"
        android:text="@string/title"
        android:textSize="22sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
 
    <EditText
        android:id="@+id/editNumber"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginTop="48dp"
        android:layout_marginEnd="24dp"
        android:hint="@string/number_hint"
        android:inputType="number"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/txtTitle" />
 
    <Button
        android:id="@+id/btnFactorial"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:text="@string/factorial"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/editNumber" />
 
</androidx.constraintlayout.widget.ConstraintLayout>
```
 
### MainActivity.java
```java
/*
Program to find factorial using Explicit Intent.
Developed by: <YOUR NAME>
Registration Number: <YOUR REG NO>
*/
package com.example.explicitintent;
 
import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
 
import androidx.appcompat.app.AppCompatActivity;
 
public class MainActivity extends AppCompatActivity {
 
    EditText editNumber;
    Button btnFactorial;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
 
        editNumber = findViewById(R.id.editNumber);
        btnFactorial = findViewById(R.id.btnFactorial);
 
        btnFactorial.setOnClickListener(v -> {
            String text = editNumber.getText().toString().trim();
 
            if (text.isEmpty()) {
                Toast.makeText(this, "Please enter a number", Toast.LENGTH_SHORT).show();
                return;
            }
 
            int num = Integer.parseInt(text);
 
            // Limit to 20 to avoid long overflow
            if (num < 0 || num > 20) {
                Toast.makeText(this, "Enter a number between 0 and 20", Toast.LENGTH_SHORT).show();
                return;
            }
 
            // Explicit intent: target class is named directly
            Intent intent = new Intent(MainActivity.this, SecondActivity.class);
            intent.putExtra("number", num);
            startActivity(intent);
        });
    }
}
```
 
### activity_second.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/second"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SecondActivity">
 
    <TextView
        android:id="@+id/txtResult"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="150dp"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
 
    <Button
        android:id="@+id/btnBack"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="48dp"
        android:text="@string/go_back"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/txtResult" />
 
</androidx.constraintlayout.widget.ConstraintLayout>
```
 
### SecondActivity.java
```java
package com.example.explicitintent;
 
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
 
import androidx.appcompat.app.AppCompatActivity;
 
public class SecondActivity extends AppCompatActivity {
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
 
        TextView txtResult = findViewById(R.id.txtResult);
        Button btnBack = findViewById(R.id.btnBack);
 
        // Receive the number sent from MainActivity
        int num = getIntent().getIntExtra("number", 0);
 
        // Compute factorial (0! = 1)
        long fact = 1;
        for (int i = 2; i <= num; i++) {
            fact *= i;
        }
 
        txtResult.setText("Factorial of " + num + " is " + fact);
 
        // Return to the first screen
        btnBack.setOnClickListener(v -> finish());
    }
}
```
 
### AndroidManifest.xml (inside `<application>`)
```xml
<activity
    android:name=".MainActivity"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
 
<activity
    android:name=".SecondActivity"
    android:exported="false" />
```
 

 
## Output

<img width="1530" height="864" alt="image" src="https://github.com/user-attachments/assets/c8a3a04e-bc49-4be9-9f75-c8a824c0b5c6" />


<img width="1534" height="863" alt="image" src="https://github.com/user-attachments/assets/4c4f96a0-86df-47c0-a7ae-7e508d40401a" />

 
## Result
Thus, an Android application with two screens was developed using an Explicit Intent. The first screen accepts a number, and the second screen displays its factorial. The application was executed successfully.
 
