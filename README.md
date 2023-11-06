Nama : Yoga Pratama

NIM  : 312210022

Kelas : TI.22.A1

Matakuliah : Pemrograman Mobile

Dosen pengajar : Donny Maulana, S.Kom., M.M.S.I.

# Fibonacci - UTS - PEMROGRAMAN MOBILE

assalamau'alaikum saya akan memberikan hasil dari bilangan fibonacci saya untuk tugas uts,dan saya merubah sedikit tampilan dari code yang tertera atau di ajarkan.
beberapa code yang di butuhkan yaitu string, Layout, MainActivity Java, dan Video  .
yang pertama adalah

## String 

String adalah resource sederhana yang direferensikan menggunakan nilai yang diberikan dalam atribut name.

Code string 
````
<resources>
    <string name="app_name">Fibonaci</string>
    <string name="button_label_finish">Toast</string>
    <string name="button_label_count">Count</string>
    <string name="toast_massage">Bilangan Fibonance</string>
    <string name="button_label_toast">angka limit Fibonacci?</string>
    <string name="count_initial_value">1</string>
</resources>
````
Code string diatas digunakan untuk bilangan fibonacci yang ada dalam layout saya.

## Layout

Layout adalah tampilan tata letak yang ada di android studio , ssedangkan code dibawah adalah Layout dari bilangan Fibonacci 

Code Layout
````
<Button
        android:id="@+id/button_toast"
        android:layout_width="390dp"
        android:layout_height="49dp"
        android:layout_marginStart="4dp"
        android:layout_marginTop="4dp"
        android:background="@color/colorPrimary"
        android:onClick="setLimit"
        android:text="@string/button_label_toast"
        android:textColor="@android:color/white"
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
        android:background="#80FF00"
        android:gravity="center_vertical"
        android:text="@string/count_initial_value"
        android:textAlignment="center"
        android:textColor="@color/colorPrimaryDark"
        android:textSize="160sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@id/button_count"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/button_toast"
        tools:ignore="RtlCompat" />
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

[Hasil Run Bilangan Fibonacci.webm](https://github.com/yogafrtm25/Fibonacci/assets/115678171/fd28a67f-3470-45a1-be2c-13f3a97108e4)





