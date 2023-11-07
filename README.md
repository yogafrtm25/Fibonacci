Nama : Yoga Pratama

NIM  : 312210022

Kelas : TI.22.A1

Matakuliah : Pemrograman Mobile

Dosen pengajar : Donny Maulana, S.Kom., M.M.S.I.


# Fibonacci - UTS - PEMROGRAMAN MOBILE

assalamau'alaikum saya akan memberikan hasil dari bilangan fibonacci saya untuk tugas uts,dan saya merubah sedikit tampilan dari code yang tertera atau di ajarkan.
beberapa code yang di butuhkan yaitu string, Layout, MainActivity Java, dan Video  .
yang pertama adalah

## Daftar Isi
| No.| DAFTAR ISI       | Menuju                                 |
|----|------------      |----------------------------------------|
| 1. | String           | [Click Here   ](#string)               |
| 2. | Color            | [Click Here   ](#color)                |
| 3. | Layout           | [Click Here   ](#layout)               |
| 4. | Java             | [Click Here   ](#mainactivity-java)    |
| 5. | Video Hasil Run  | [Click Here   ](#video-hasil-run)      |


## String 

String adalah resource sederhana yang direferensikan menggunakan nilai yang diberikan dalam atribut name.

Code string 
````
<resources>
    <string name="app_name">Fibonaci</string>
    <string name="button_label_finish">Back</string>
    <string name="button_label_count">Count</string>
    <string name="toast_massage">Bilangan Fibonance</string>
    <string name="button_label_toast">Set Limit?</string>
    <string name="count_initial_value">1</string>
</resources>
````
Code string diatas digunakan untuk bilangan fibonacci yang ada dalam layout saya.

## Color
 
 Color adalah untuk menambahkan warna di dalam aplikasi nya 
 Code Color
 ````
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="colorPrimary">#3F5185</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
</resources>
````

## Layout

Layout adalah tampilan tata letak yang ada di android studio , ssedangkan code dibawah adalah Layout dari bilangan Fibonacci 

Code Layout
````
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:background="@drawable/ahay"
    >


    <Button
        android:id="@+id/button_toast"
        android:layout_width="380dp"
        android:layout_height="49dp"
        android:layout_marginTop="16dp"
        android:background="@color/colorPrimary"
        android:onClick="setLimit"
        android:text="@string/button_label_toast"
        android:textColor="@android:color/white"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/button_count"
        android:layout_width="190dp"
        android:layout_height="48dp"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:background="@color/colorPrimary"
        android:onClick="countUp"
        android:text="@string/button_label_count"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        tools:ignore="UsingOnClickInXml,VisualLintButtonSize" />

    <Button
        android:id="@+id/button_finish"
        android:layout_width="190dp"
        android:layout_height="48dp"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:background="@color/colorPrimary"
        android:onClick="back1"
        android:text="@string/button_label_finish"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        tools:ignore="UsingOnClickInXml" />

    <TextView
        android:id="@+id/show_count"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:gravity="center_vertical"
        android:text="@string/count_initial_value"
        android:textAlignment="center"
        android:textColor="@color/colorPrimaryDark"
        android:textSize="160sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@id/button_count"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/button_toast"
        app:layout_constraintVertical_bias="1.0"
        tools:ignore="RtlCompat" />

</androidx.constraintlayout.widget.ConstraintLayout>
````

## MainActivity Java

saya disini akan menggunakan code java dari bilangan fibonacci.

Code java Bilangan Fibonacci  

````
package com.example.fibonaci;


import android.app.AlertDialog;
import android.content.DialogInterface;
import android.graphics.Color;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    private TextView showCount;
    private int count = 1;
    private long fibNMinus1 = 1;
    private long fibNMinus2 = 1;
    private int limit = -1; // Inisialisasi limit dengan nilai default

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        showCount = findViewById(R.id.show_count);
    }

    public void countUp(View view) {
        if (count == 0) {
            showCount.setText("0");
        } else if (count == 1) {
            showCount.setText("1");
        } else {
            if (limit != -1 && count > limit) {
                // Jika count melebihi limit, atur ulang perhitungan
                count = 0;
                fibNMinus1 = 1;
                fibNMinus2 = 0;
                showCount.setText(getString(R.string.count_initial_value));
            } else {
                long fibCurrent = fibNMinus1 + fibNMinus2;
                fibNMinus2 = fibNMinus1;
                fibNMinus1 = fibCurrent;

                // Mengubah warna teks menjadi warna RGB dengan warna yang berbeda setiap kali angka berubah
                int red = (int) (Math.random() * 256);
                int green = (int) (Math.random() * 256);
                int blue = (int) (Math.random() * 256);
                showCount.setTextColor(Color.rgb(red, green, blue));

                showCount.setText(String.valueOf(fibCurrent));
            }
        }

        count++;
    }

    public void back1(View view) {
        count = 1;
        fibNMinus1 = 1;
        fibNMinus2 = 0;
        showCount.setText(getString(R.string.count_initial_value));
    }

    public void setLimit(View view) {
        // Create and display a dialog to set the limit
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Set Limit");

        final EditText input = new EditText(this);
        input.setInputType(android.text.InputType.TYPE_CLASS_NUMBER);
        builder.setView(input);

        builder.setPositiveButton("OK", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                // Get the limit from the input and set it for calculations
                String limitStr = input.getText().toString();
                limit = Integer.parseInt(limitStr);
            }
        });

        builder.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                dialog.cancel();
            }
        });


        builder.show();
    }
}
````

## Video Hasil Run

[hasin run.webm](https://github.com/yogafrtm25/Fibonacci/assets/115678171/999855d2-949c-4f3c-8dea-be9b5ba538d7)




Sekian dari saya 
## Terima Kasih  


