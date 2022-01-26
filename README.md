# BMI. XML <!-- Linear layout start here -->

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"

android:layout_width="fill_parent"

android:layout_height="fill_parent"

android:background="@drawable/green_back"

android:fadingEdge="horizontal"

android:orientation="vertical" >

<!-- Text view for BMI Text -->

<TextView

android:id="@+id/tv1"

android:layout_width="124dp"

android:layout_height="wrap_content"

android:layout_gravity="center"

android:paddingLeft="15dp"

android:paddingTop="40dp"

android:shadowColor="@android:color/black"

android:shadowDx="4"

android:shadowDy="4"

android:text="BMI"

android:textAppearance="?android:attr/textAppearanceLarge"

android:textColor="@android:color/white"

android:textSize="50sp"

android:typeface="serif" />

<!-- Textview for calculator text -->

<TextView

android:id="@+id/tv2"

android:layout_width="wrap_content"

android:layout_height="wrap_content"

android:layout_gravity="center"

android:text="Calculator"

android:textColor="@android:color/white"

android:textSize="20dp"

android:textStyle="bold" />

<!-- Textview for WEIGHT(KG) text -->

<TextView

android:id="@+id/tv3"

android:layout_width="wrap_content"

android:layout_height="wrap_content"

android:layout_gravity="center"

android:paddingTop="30dp"

android:text="WEIGHT (KG)"

android:textAppearance="?android:attr/textAppearanceMedium"

android:textColor="@android:color/white"

android:textStyle="bold|italic"

android:typeface="serif" />

<!-- Edit text for entering weight with hint in kgs -->

<EditText

android:id="@+id/et1"

android:layout_width="96dp"

android:layout_height="wrap_content"

android:layout_gravity="center"

android:hint="IN KGs"

android:ems="10"

android:fadingEdgeLength="10dp"

android:inputType="numberDecimal"

android:textAlignment="center" >

<requestFocus />

</EditText>

<!-- Text view for HEIGHT(CM)text -->

<TextView

android:id="@+id/tv3"

android:layout_width="wrap_content"

android:layout_height="wrap_content"

android:layout_gravity="center"

android:paddingTop="30dp"

android:text="HEIGHT (CM)"

android:textAppearance="?android:attr/textAppearanceMedium"

android:textColor="@android:color/white"

android:textStyle="bold|italic"

android:typeface="serif" />

<!-- Edit text for entering height with hint in cm -->

<EditText

android:id="@+id/et2"

android:layout_width="96dp"

android:layout_height="wrap_content"

android:layout_gravity="center"

android:hint="IN CMs"

android:ems="10"

android:inputType="numberDecimal" >

</EditText>

<!-- Button for calculating the formula, when pressed, with calculate written over it -->

<Button

android:id="@+id/ib1"

android:layout_width="158dp"

android:layout_height="51dp"

android:layout_gravity="center"

android:layout_marginTop="20dp"

android:fadingEdge="vertical"

android:longClickable="true"

android:nextFocusRight="@color/black"

android:text="Calculate"

android:visibility="visible" />

<!-- Text view for showing result -->

<TextView

android:id="@+id/tv4"

android:layout_width="wrap_content"

android:layout_height="wrap_content"

android:layout_gravity="center"

android:paddingTop="20dp"

android:text=""

android:textSize="20dp"

android:textStyle="bold"

android:textColor="@android:color/holo_orange_dark"/>
Java 
  //Import necessary package and file

package com.magnetbrains;

import com.magnetbrains.R;

import android.os.Bundle;

import android.app.Activity;

import android.text.TextUtils;

import android.view.Menu;

import android.view.View;

import android.widget.EditText;

import android.widget.TextView;

//Main activity class start here

public class MainActivity extends Activity {

//Define layout

@Override

protected void onCreate(Bundle savedInstanceState) {

super.onCreate(savedInstanceState);

setContentView(R.layout.activity_main);

// Get the references to the widgets

final EditText e1 = (EditText) findViewById(R.id.et1);

final EditText e2 = (EditText) findViewById(R.id.et2);

final TextView tv4 = (TextView) findViewById(R.id.tv4);

findViewById(R.id.ib1).setOnClickListener(new View.OnClickListener() {

// Logic for validation, input can't be empty

@Override

public void onClick(View v) {

String str1 = e1.getText().toString();

String str2 = e2.getText().toString();

if(TextUtils.isEmpty(str1)){

e1.setError("Please enter your weight");

e1.requestFocus();

return;

}

if(TextUtils.isEmpty(str2)){

e2.setError("Please enter your height");

e2.requestFocus();

return;

}

//Get the user values from the widget reference

float weight = Float.parseFloat(str1);

float height = Float.parseFloat(str2)/100;

//Calculate BMI value

float bmiValue = calculateBMI(weight, height);

//Define the meaning of the bmi value

String bmiInterpretation = interpretBMI(bmiValue);

tv4.setText(String.valueOf(bmiValue + "-" + bmiInterpretation));

}

});

}

//Calculate BMI

private float calculateBMI (float weight, float height) {

return (float) (weight / (height * height));

}

// Interpret what BMI means

private String interpretBMI(float bmiValue) {

if (bmiValue < 16) {

return "Severely underweight";

} else if (bmiValue < 18.5) {

return "Underweight";

} else if (bmiValue < 25) {

return "Normal";

} else if (bmiValue < 30) {

return "Overweight";

} else {

return "Obese";

}

}

}
</LinearLayout>

