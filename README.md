# Ex.No:4 Develop a simple application to display the avaliable sensor in android mobile devices using Sensor Manager in android studio.


## AIM:

To develop a sensor application to use the sensor manager class to identify and get the list of available sensors on a device. in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Giraffe)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as Sensor and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display avaliable sensor in android mobile devices.

Step 7: Save and run the application.

## PROGRAM:
```

Program to print the avaliable sensor in android mobile devices”.
Developed by: Swetha A 
Registeration Number : 212223220114

```

### Activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>

<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#090D1A">


    <View
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:background="@drawable/sensor_glow"
        android:alpha="0.3"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fillViewport="true">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:padding="22dp">


            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="ANDROID SENSOR LAB"
                android:textColor="#8B9EFF"
                android:textSize="12sp"
                android:textStyle="bold"
                android:letterSpacing="0.15"
                android:layout_marginTop="12dp" />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Sensor Hub"
                android:textColor="#FFFFFF"
                android:textSize="34sp"
                android:textStyle="bold"
                android:layout_marginTop="6dp" />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Discover the sensors inside your device"
                android:textColor="#858DA5"
                android:textSize="14sp"
                android:layout_marginTop="4dp"
                android:layout_marginBottom="22dp" />

            <!-- Total Sensor Card -->

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="150dp"
                android:orientation="vertical"
                android:gravity="center"
                android:background="@drawable/total_card"
                android:padding="20dp">

                <TextView
                    android:id="@+id/tvTotalSensors"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="0"
                    android:textColor="#FFFFFF"
                    android:textSize="42sp"
                    android:textStyle="bold" />

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="SENSORS DETECTED"
                    android:textColor="#9DA6C1"
                    android:textSize="12sp"
                    android:textStyle="bold"
                    android:letterSpacing="0.12"
                    android:layout_marginTop="4dp" />

            </LinearLayout>



            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal"
                android:gravity="center_vertical"
                android:layout_marginTop="25dp"
                android:layout_marginBottom="12dp">

                <TextView
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:text="AVAILABLE SENSORS"
                    android:textColor="#FFFFFF"
                    android:textSize="16sp"
                    android:textStyle="bold" />

                <TextView
                    android:id="@+id/tvStatus"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="LIVE"
                    android:textColor="#6CFF9B"
                    android:textSize="11sp"
                    android:textStyle="bold" />

            </LinearLayout>


            <LinearLayout
                android:id="@+id/sensorContainer"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="vertical" />


            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal"
                android:gravity="center_vertical"
                android:padding="16dp"
                android:layout_marginTop="18dp"
                android:layout_marginBottom="20dp"
                android:background="@drawable/info_bottom">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="●"
                    android:textColor="#6CFF9B"
                    android:textSize="17sp" />

                <TextView
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:text="SensorManager connected"
                    android:textColor="#B8C0D5"
                    android:textSize="13sp"
                    android:layout_marginStart="10dp" />

            </LinearLayout>

        </LinearLayout>

    </ScrollView>

</androidx.constraintlayout.widget.ConstraintLayout>

```
### MainActivity.java
```
package com.example.sensorhub;

import android.hardware.Sensor;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.view.Gravity;
import android.widget.LinearLayout;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import java.util.List;

public class MainActivity extends AppCompatActivity {

    private SensorManager sensorManager;

    private TextView tvTotalSensors;
    private TextView tvStatus;
    private LinearLayout sensorContainer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        tvTotalSensors = findViewById(R.id.tvTotalSensors);
        tvStatus = findViewById(R.id.tvStatus);
        sensorContainer = findViewById(R.id.sensorContainer);

        sensorManager =
                (SensorManager) getSystemService(SENSOR_SERVICE);

        displayAvailableSensors();
    }

    private void displayAvailableSensors() {

        List<Sensor> sensors =
                sensorManager.getSensorList(
                        Sensor.TYPE_ALL
                );

        tvTotalSensors.setText(
                String.valueOf(sensors.size())
        );

        if (sensors.isEmpty()) {

            tvStatus.setText("NONE");

            TextView emptyMessage = new TextView(this);

            emptyMessage.setText(
                    "No sensors were detected on this device."
            );

            emptyMessage.setTextColor(
                    getColor(android.R.color.white)
            );

            emptyMessage.setTextSize(15);

            emptyMessage.setGravity(Gravity.CENTER);

            emptyMessage.setPadding(
                    20, 40, 20, 40
            );

            sensorContainer.addView(emptyMessage);

            return;
        }

        for (Sensor sensor : sensors) {

            addSensorCard(sensor);
        }
    }

    private void addSensorCard(Sensor sensor) {

        LinearLayout card =
                new LinearLayout(this);

        card.setOrientation(
                LinearLayout.HORIZONTAL
        );

        card.setGravity(
                Gravity.CENTER_VERTICAL
        );

        card.setPadding(
                20, 18, 20, 18
        );

        card.setBackgroundResource(
                R.drawable.sensor_item
        );

        LinearLayout.LayoutParams cardParams =
                new LinearLayout.LayoutParams(
                        LinearLayout.LayoutParams.MATCH_PARENT,
                        LinearLayout.LayoutParams.WRAP_CONTENT
                );

        cardParams.setMargins(
                0, 0, 0, 12
        );

        card.setLayoutParams(cardParams);

        TextView icon =
                new TextView(this);

        icon.setText("◈");
        icon.setTextSize(25);
        icon.setTextColor(
                getColor(android.R.color.holo_blue_light)
        );

        LinearLayout.LayoutParams iconParams =
                new LinearLayout.LayoutParams(
                        55,
                        55
                );

        icon.setGravity(Gravity.CENTER);

        card.addView(icon, iconParams);

        LinearLayout textContainer =
                new LinearLayout(this);

        textContainer.setOrientation(
                LinearLayout.VERTICAL
        );

        LinearLayout.LayoutParams textParams =
                new LinearLayout.LayoutParams(
                        0,
                        LinearLayout.LayoutParams.WRAP_CONTENT,
                        1
                );

        textParams.setMargins(
                14, 0, 0, 0
        );

        TextView sensorName =
                new TextView(this);

        sensorName.setText(
                sensor.getName()
        );

        sensorName.setTextColor(
                getColor(android.R.color.white)
        );

        sensorName.setTextSize(15);
        sensorName.setMaxLines(2);
        
        
        TextView vendor =
                new TextView(this);

        vendor.setText(
                "Vendor: " + sensor.getVendor()
        );

        vendor.setTextColor(
                getColor(android.R.color.darker_gray)
        );

        vendor.setTextSize(11);

        vendor.setMaxLines(1);

        textContainer.addView(sensorName);

        textContainer.addView(vendor);

        card.addView(
                textContainer,
                textParams
        );

        
        TextView sensorType =
                new TextView(this);

        sensorType.setText(
                "TYPE " + sensor.getType()
        );

        sensorType.setTextColor(
                getColor(android.R.color.holo_green_light)
        );

        sensorType.setTextSize(10);
        sensorType.setGravity(Gravity.CENTER);

        card.addView(sensorType);

        sensorContainer.addView(card);
    }
}
```

## OUTPUT


<img width="1917" height="1078" alt="Screenshot 2026-08-25 091822" src="https://github.com/user-attachments/assets/bdfc2921-4365-4f43-a160-0b686d89104b" />

## Execution: 

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/9db7a012-d0eb-4a63-b937-8862f3757010" />

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/03bdc27f-a4a3-4ac2-8240-f7f60d5feec5" />




## RESULT
Thus a Simple Android Application to display the avaliable sensor in android mobile devices using Sensor Manager in Android Studio is developed and executed successfully.
